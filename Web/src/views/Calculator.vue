<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import RuleInput from '../components/RuleInput.vue'
import type { Rule } from '../Logic/Rule'

const selectedRules = ref([])

const suspensionRules = {
  r6_2_1: {
    refNumer: '6.2.1',
    description: 'Height Adjustabled Coil-overs',
    points: 25,
  },
  r6_2_2: {
    refNumer: '6.2.2',
    description: 'Springs Stage 2 (Any spring combination beyond Stage 1)',
    points: 13,
  },
  r6_2_3: {
    refNumer: '6.2.3',
    description: 'Springs Stage 1 (OEM style: Up to 30% rate increase and/or lowered 25mm or less)',
    points: 7,
  },
  r6_2_4: {
    refNumer: '6.2.4',
    description: 'Seam Weld',
    points: 10
  },
  r6_2_5: {
    refNumer: '6.2.5',
    description: 'Dampers (performance shocks, re-valved, non OEM, Modified bodies)',
    points: 7,
  },
  r6_2_6: {
    refNumer: '6.2.6',
    description: 'Change suspension type and/or alternate mounting points',
    points: 10,
  },
  r6_2_7: {
    refNumer: '6.2.7',
    description: 'Roll Cage / Chassis Bracing (6 or more attachment points)',
    points: 5,
  },
  r6_2_8: {
    refNumer: '6.2.8',
    description: 'Sway Bars (1 bar, no points for modification to the bar and links)',
    points: 2,
  },
  r6_2_9: {
    refNumer: '6.2.9',
    description: 'Sway Bars (both, no points for modification to the bar and links)',
    points: 6,
  },
  r6_2_10: {
    refNumer: '6.2.10',
    description: 'Camber plates, bushing or bolts with camber adjustment allowance',
    points: 3,
  },
  r6_2_11: {
    refNumer: '6.2.11',
    description: 'Spherical bearing ( on control arms )',
    points: 5,
  },
  r6_2_12: {
    refNumer: '6.2.12',
    description: 'Subframe modifications or its mounts and/or bushings',
    points: 5,
  }
};

const allRules: Array<any> = []

addRules(suspensionRules);

const pointsToAdd = computed(() => {
  const points = selectedRules.value.map((r) => {
    const rule = allRules.find((el) => el.refNumer === r)
    return rule ? rule.points : 0
  })
  const totalPoints = points.reduce((acc, curr) => acc + curr, 0)
  return totalPoints
})


function addRules(rulesContainer: any) {
  for (const [_, value] of Object.entries(rulesContainer)) {
    if (typeof value === 'string') {
    } else {
      allRules.push(value);
    }
  }
}
</script>

<template>
  <div>
    <div class="heading">
      <h1>NASA Autocross Class Calculator</h1>
    </div>

    <div>selected rules: {{ selectedRules }}</div>
    <div>points: {{ pointsToAdd }}</div>

    <div class="container">
      <h2 class="header">Chassis and Suspension</h2>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_1"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_2"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_3"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_4"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_5"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_6"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_7"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_8"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_9"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_10"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_11"></rule-input>
      <rule-input v-model="selectedRules" :rule="suspensionRules.r6_2_12"></rule-input>
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

.container {
  padding-top: 20px;
}

.rule {
  display: grid;
  grid-template-columns: 20px 30px auto;
}

.header {
  grid-row: 1;
  grid-column: 1 / span 3;
}
</style>
