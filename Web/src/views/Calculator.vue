<script setup lang="ts">

import { reactive, ref } from 'vue';
import { Rule } from '../Logic/Rule'

  const selectedRules = ref([]);

  var r6_2_1: Rule = {
    refNumer: "6.2.1",
    description: "Height Adjustabled Coil-overs",
    points: 25,
  }
  var r6_2_2: Rule = {
    refNumer: "6.2.2",
    description: "Springs Stage 1 (OEM style: Up to 30% rate increase and/or lowered 25mm or less)",
    points: 7,
  }
</script >

<template>
  <div>
    <div class="heading">
      <h1>NASA Autocross Class Calculator</h1>
    </div>

    <div>
      selected rules: {{ selectedRules }}
    </div>

    <div class="container">
      <div class="header">Chassis and Suspension</div>
      <div class="rule">
        <div>{{r6_2_1.description}}</div>
        <div>{{r6_2_1.points}}</div>
        <div>
          <input type="checkbox" :value="r6_2_1.refNumer" v-model="selectedRules"/>
        </div>
      </div>
      <div class="rule">
        <div>{{r6_2_2.description}}</div>
        <div>{{r6_2_2.points}}</div>
        <div><input type="checkbox" :value="r6_2_2.refNumer" v-model="selectedRules" /></div>
      </div>
      <div class="rule">
        <div>Springs Stage 2 (Any spring combination beyond Stage 1)</div>
        <div>13</div>
        <div><input type="checkbox" /></div>
      </div>
      <div class="rule">
        <div>Seam weld</div>
        <div>10</div>
        <div><input type="checkbox" /></div>
      </div>
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
