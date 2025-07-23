<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import RuleInput from '../components/RuleInput.vue'
import type { Rule } from '../Logic/Rule'

const selectedRules = ref([])

const r6_2_1: Rule = {
  refNumer: '6.2.1',
  description: 'Height Adjustabled Coil-overs',
  points: 25,
}
const r6_2_2: Rule = {
  refNumer: '6.2.2',
  description: 'Springs Stage 1 (OEM style: Up to 30% rate increase and/or lowered 25mm or less)',
  points: 7,
}
const r6_2_3: Rule = {
  refNumer: '6.2.3',
  description: 'Seam Weld',
  points: 10
}

const allRules = [r6_2_1, r6_2_2, r6_2_3]

const pointsToAdd = computed(() => {
  const points = selectedRules.value.map((r) => {
    const rule = allRules.find((el) => el.refNumer === r)
    return rule ? rule.points : 0
  })
  const totalPoints = points.reduce((acc, curr) => acc + curr, 0)
  return totalPoints
})
</script>

<template>
  <div>
    <div class="heading">
      <h1>NASA Autocross Class Calculator</h1>
    </div>

    <div>selected rules: {{ selectedRules }}</div>
    <div>points: {{ pointsToAdd }}</div>

    <div class="container">
      <div class="header">Chassis and Suspension</div>
      <rule-input v-model="selectedRules" :rule="r6_2_1"></rule-input>
      <rule-input v-model="selectedRules" :rule="r6_2_2"></rule-input>
      <rule-input v-model="selectedRules" :rule="r6_2_3"></rule-input>
      <div class="rule">
        <div>Change Suspension Type and/or alternate mounting points.</div>
        <div>10</div>
        <div><input type="checkbox" /></div>
      </div>
      <div class="rule">
        <div>Roll cage / Chassis Bracing (6 or mor attachment points)</div>
        <div>5</div>
        <div><input type="checkbox" /></div>
      </div>
      <div class="rule">
        <div>Sway bars (1 bar, no points for modification to the bar and links)</div>
        <div>2</div>
        <div><input type="checkbox" /></div>
      </div>
      <div class="rule">
        <div>Sway bars (both, no points for modification to the bar and links)</div>
        <div>6</div>
        <div><input type="checkbox" /></div>
      </div>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .heading {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

.rule {
  display: grid;
  grid-template-columns: auto 50px 50px;
}

.header {
  grid-row: 1;
  grid-column: 1 / span 3;
}
</style>
