<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import RuleInput from '../components/RuleInput.vue'
import type { Rule } from '../Logic/Rule'

const selectedRules = ref([])

const suspensionRules = {
  r6_2_1: {
    refNumber: '6.2.1',
    description: 'Height Adjustabled Coil-overs',
    points: 25,
  },
  r6_2_2: {
    refNumber: '6.2.2',
    description: 'Springs Stage 2 (Any spring combination beyond Stage 1)',
    points: 13,
  },
  r6_2_3: {
    refNumber: '6.2.3',
    description: 'Springs Stage 1 (OEM style: Up to 30% rate increase and/or lowered 25mm or less)',
    points: 7,
  },
  r6_2_4: {
    refNumber: '6.2.4',
    description: 'Seam Weld',
    points: 10
  },
  r6_2_5: {
    refNumber: '6.2.5',
    description: 'Dampers (performance shocks, re-valved, non OEM, Modified bodies)',
    points: 7,
  },
  r6_2_6: {
    refNumber: '6.2.6',
    description: 'Change suspension type and/or alternate mounting points',
    points: 10,
  },
  r6_2_7: {
    refNumber: '6.2.7',
    description: 'Roll Cage / Chassis Bracing (6 or more attachment points)',
    points: 5,
  },
  r6_2_8: {
    refNumber: '6.2.8',
    description: 'Sway Bars (1 bar, no points for modification to the bar and links)',
    points: 2,
  },
  r6_2_9: {
    refNumber: '6.2.9',
    description: 'Sway Bars (both, no points for modification to the bar and links)',
    points: 6,
  },
  r6_2_10: {
    refNumber: '6.2.10',
    description: 'Camber plates, bushing or bolts with camber adjustment allowance',
    points: 3,
  },
  r6_2_11: {
    refNumber: '6.2.11',
    description: 'Spherical bearing ( on control arms )',
    points: 5,
  },
  r6_2_12: {
    refNumber: '6.2.12',
    description: 'Subframe modifications or its mounts and/or bushings',
    points: 5,
  }
};
const bodyRules = {
  r6_3_1: {
    refNumber: '6.3.1',
    description: 'Glass Removal (other than sunroof)',
    points: 5
  },
  r6_3_2: {
    refNumber: '6.3.2',
    description: 'Removal of interior coverings, seats',
    points: 3
  },
  r6_3_3: {
    refNumber: '6.3.3',
    description: 'Lightweight hood',
    points: 2
  },
  r6_3_4: {
    refNumber: '6.3.4',
    description: 'Lightweight trunk or hatch',
    points: 2
  },
  r6_3_5: {
    refNumber: '6.3.5',
    description: 'Sunroof and/or window mechanism removal',
    points: 2
  },
  r6_3_6: {
    refNumber: '6.3.6',
    description: 'Racing Seat (Non OE and 1. homologated by any racing sanctioning body; and/or 2. weighs less than 20 lbs',
    points: 2
  },
  r6_3_7: {
    refNumber: '6.3.7',
    description: 'Non-factory body flares to allow wide tires',
    points: 2
  },
  r6_3_8: {
    refNumber: '6.3.8',
    description: 'Lightweight fenders and/or body panels',
    points: 2
  },
  r6_3_9: {
    refNumber: '6.3.9',
    description: 'Heating and AC removal',
    points: 2
  },
  r6_3_10: {
    refNumber: '6.3.10',
    description: 'Light(s) removal',
    points: 1
  },
  r6_3_11: {
    refNumber: '6.3.11',
    description: 'Lightweight battery, 15lbs or less',
    points: 1
  },
  r6_3_12: {
    refNumber: '6.3.12',
    description: 'Airbag(s) and or speaker(s) removal',
    points: 1
  },
  r6_3_13: {
    refNumber: '6.3.13',
    description: 'Reduced weight brake components (rotor and or caliper)',
    points: 1
  },
  r6_3_14: {
    refNumber: '6.3.14',
    description: 'Removing wipers, door locks, mirrors and/or window motors, side impact beams',
    points: 2
  },
  r6_3_15: {
    refNumber: '6.3.15',
    description: 'Cutting out body structure (floor, cowl, pillars, etc)',
    points: 10
  }
}
const aeroRules = {
  r6_4_1: {
    refNumber: '6.4.1',
    description: 'Vehicles 2200 lbs or less (with Driver)',
    points: 10
  },
  r6_4_2: {
    refNumber: '6.4.2',
    description: 'Vehicles 2201-3200 lbs (with Driver)',
    points: 5
  }
}

const allRules: Array<any> = []

addRules(suspensionRules);
addRules(bodyRules);
addRules(aeroRules);

const pointsToAdd = computed(() => {
  const points = selectedRules.value.map((r) => {
    const rule = allRules.find((el) => el.refNumber === r)
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

    <div class="container">
      <h2 class="header">Body and Weight Reduction</h2>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_1"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_2"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_3"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_4"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_5"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_6"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_7"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_8"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_9"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_10"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_11"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_12"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_13"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_14"></rule-input>
      <rule-input v-model="selectedRules" :rule="bodyRules.r6_3_15"></rule-input>
    </div>
    <div class="container">
      <h2 class="header">Aero (other than OEM add-ons)</h2>
      <div>
        Aero mods include installation of aftermarket devices to improve performance by
        improving aerodynamics and/or increasing downforce:
        <ul>
          <li>Wings: front or rear with area greater than 240 sq in </li>
          <li>Splitters: extend 4 inch or more beyond frontal bumper of the vehicle</li>
        </ul>
      </div>
      <rule-input v-model="selectedRules" :rule="aeroRules.r6_4_1"></rule-input>
      <rule-input v-model="selectedRules" :rule="aeroRules.r6_4_2"></rule-input>
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
