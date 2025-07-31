<script setup lang="ts">
import { reactive, ref, computed } from 'vue'
import RuleInput from '../components/RuleInput.vue'
import type { Rule } from '../Logic/Rule'

const selectedRules = ref([])
const baseClass = ref('');
const basePoints = ref('');
const index = ref('');

const pointsToAdd = computed(() => {
  const points = selectedRules.value.map((r) => {
    const rule = allRules.find((el) => el.refNumber === r)
    return rule ? rule.points : 0
  })
  return points.reduce((acc, curr) => acc + curr, 0)
})
const totalPoints = computed(() => {
  var baseClassPoints = Number(baseClass.value);
  var basePointsPoints = Number(basePoints.value);
  var pointsToAddPoints = Number(pointsToAdd.value);
  var indexPoints = Number(index.value) > 0 ? Number(index.value) : 1.0;

  return baseClassPoints + basePointsPoints + (pointsToAddPoints * indexPoints);
});
const newClass = computed(() => {
  const total = Math.round(totalPoints.value);
  const nextClass = classes.findIndex((c) => c.points > total);
  return nextClass !== -1 ? classes[nextClass - 1].name : '???';
});

var classes = [
  { name: 'G', points: 0 },
  { name: 'F', points: 20 },
  { name: 'E', points: 40 },
  { name: 'D', points: 60 },
  { name: 'C', points: 80 },
  { name: 'B', points: 100 },
  { name: 'A', points: 120 },
  { name: 'R', points: 150 },
  { name: 'X', points: 190 },
  { name: '0', points: 250 },
];


const isNumeric = (val: string): boolean => {
  return !isNaN(Number(val));
}

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
const drivetrainRules = {
  r6_5_2: {
    refNumber: '6.5.2',
    description: 'Change of drivetrain configuration ( FWD to AWD, RWD to AWD, AWD to RWD, etc.)',
    points: 15,
  },
  r6_5_3: {
    refNumber: '6.5.3',
    description: 'Transmission swap (if gear ratios of 1, 2 differ and/or weight reduced by 20 or more lbs)',
    points: 5,
  },
  r6_5_4: {
    refNumber: '6.5.4',
    description: 'Change final drive ratio',
    points: 3,
  },
  r6_5_5: {
    refNumber: '6.5.5',
    description: 'Differential upgrade LSD ',
    points: 5,
  },
  r6_5_6: {
    refNumber: '6.5.6',
    description: 'Engine bore or stroke modification',
    points: 5,
  },
  r6_5_7: {
    refNumber: '6.5.7',
    description: 'Compression ratio change',
    points: 4,
  },
  r6_5_8: {
    refNumber: '6.5.8',
    description: 'Cylinder head porting; upsizing and/or modifying valves; or rotary engine porting',
    points: 4,
  },
  r6_5_9: {
    refNumber: '6.5.9',
    description: 'Non OE engine pulley(s) ( size or weight)',
    points: 2,
  },
  r6_5_10: {
    refNumber: '6.5.10',
    description: 'Flywheel / Clutch weight reduction',
    points: 2,
  },
  r6_5_11: {
    refNumber: '6.5.11',
    description: 'Non OE electric water pump',
    points: 1,
  },
  r6_5_12: {
    refNumber: '6.5.12',
    description: 'Relocation of engine/transmission 4" or more from original location',
    points: 5,
  },
  r6_5_13: {
    refNumber: '6.5.13',
    description: 'Relocation of engine/transmission 1" to 4" from original location',
    points: 2,
  },
}
const forcedInductionRules = {
  r6_6_1: {
    refNumber: '6.6.1',
    description: 'Intake ( prior to compressor )',
    points: 2,
  },
  r6_6_2: {
    refNumber: '6.6.2',
    description: 'Intercooler & piping changes',
    points: 3,
  },
  r6_6_3: {
    refNumber: '6.6.3',
    description: 'Exhaust (Cat back only)',
    points: 2,
  },
  r6_6_4: {
    refNumber: '6.6.4',
    description: 'Exhaust (Header(s), Turbo back including cat)',
    points: 5,
  },
  r6_6_5: {
    refNumber: '6.6.5',
    description: 'ECU reprogrammed, stand alone, chip, tune, etc',
    points: 10,
  },
  r6_6_6: {
    refNumber: '6.6.6',
    description: 'Turbo or supercharger modifications or upgrades',
    points: 3,
  },
  r6_6_7: {
    refNumber: '6.6.7',
    description: 'Water or methanol injection',
    points: 2,
  },
  r6_6_8: {
    refNumber: '6.6.8',
    description: 'Fuel (E85, 100+ Octane Race Gas)',
    points: 5,
  },
}
const naRules = {
  r6_7_1: {
    refNumber: '6.7.1',
    description: 'Intake manifold(s)',
    points: 3,
  },
  r6_7_2: {
    refNumber: '6.7.2',
    description: 'Intake (from manifold to filter element)',
    points: 1,
  },
  r6_7_3: {
    refNumber: '6.7.3',
    description: 'Exhaust - Any modification after the Cat (muffler(s) resonator(s), pipe(s))',
    points: 1,
  },
  r6_7_4: {
    refNumber: '6.7.4',
    description: 'Exhaust - manifold, headers, catalytic convertor',
    points: 2,
  },
  r6_7_5: {
    refNumber: '6.7.5',
    description: 'Camshafts, rocker arms',
    points: 3,
  },
  r6_7_6: {
    refNumber: '6.7.6',
    description: 'ECU reprogrammed, stand alone, chip, tune, etc',
    points: 2,
  },
  r6_7_7: {
    refNumber: '6.7.7',
    description: 'Head swapping for different design; machining or porting; valves up sizing or modifications',
    points: 4,
  },
  r6_7_8: {
    refNumber: '6.7.8',
    description: 'Rotary engine porting',
    points: 4
  },
  r6_7_9: {
    refNumber: '6.7.9',
    description: 'Fuel (E85, 100+ Octane Race Gas)',
    points: 3,
  },
}
const wheelTireRules = {
  r6_8_1: {
    refNumber: '6.8.1',
    description: 'Wheels and or tires extend beyond fenders',
    points: 5,
  },
  r6_8_2: {
    refNumber: '6.8.2',
    description: 'Wheel width increase - more than 1" over stock',
    points: 5,
  },
  r6_8_3: {
    refNumber: '6.8.3',
    description: 'Wheel width increase - up to 1" beyond stock',
    points: 2,
  },
  r6_8_4: {
    refNumber: '6.8.4',
    description: 'UTQG 50 and below (commonly known as tire treadwear rating)',
    points: 45,
  },
  r6_8_5: {
    refNumber: '6.8.5',
    description: 'UTQG 51-220',
    points: 5,
  },
  r6_8_6: {
    refNumber: '6.8.6',
    description: 'Non DOT Rated',
    points: 15,
  },
}

const allRules: Array<any> = []

addRules(suspensionRules);
addRules(bodyRules);
addRules(aeroRules);
addRules(drivetrainRules);
addRules(forcedInductionRules);
addRules(naRules);
addRules(wheelTireRules);




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

    <div class="pointsOverlay pointsOverlay--bottom">
      <div>Base Class: {{ baseClass }}</div>
      <div>Base Points: {{ basePoints }}</div>
      <div>index: {{ index }}</div>
      <div>points: {{ pointsToAdd }}</div>
      <div>Total Points: {{ Math.round(totalPoints * 100) / 100 }}</div>
      <div>New Class: {{ newClass }}</div>
    </div>

    <div class="CarInformation">
      <select v-model="baseClass">
        <option value="">Select Base Class</option>
        <option value="0">G</option>
        <option value="20">F</option>
        <option value="40">E</option>
        <option value="60">D</option>
        <option value="80">C</option>
        <option value="100">B</option>
        <option value="120">A</option>
        <option value="150">R</option>
        <option value="190">X</option>
        <option value="250">O</option>
      </select>
      <select v-model="basePoints">
        <option value="">Select Base Points</option>
        <option value="0">none</option>
        <option value="5">*</option>
        <option value="10">**</option>
        <option value="15">***</option>
      </select>
      <select v-model="index">
        <option value="">Select Tier</option>
        <option value="0.87">T1</option>
        <option value="0.92">T2</option>
        <option value="1">T3</option>
      </select>
    </div>

    <div class="rulesSections">

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

      <div class="container">
        <h2 class="header">Drivetrain and Engine Modifications</h2>
        <div>
          Adding a Turbo or Supercharder requires you to apply for a new BASE CLASS.
        </div>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_2"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_3"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_4"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_5"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_6"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_7"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_8"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_9"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_10"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_11"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_12"></rule-input>
        <rule-input v-model="selectedRules" :rule="drivetrainRules.r6_5_13"></rule-input>
      </div>

      <div class="container">
        <h2 class="header">Supercharged and or Turbo Vehicles</h2>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_1"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_2"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_3"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_4"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_5"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_6"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_7"></rule-input>
        <rule-input v-model="selectedRules" :rule="forcedInductionRules.r6_6_8"></rule-input>
      </div>

      <div class="container">
        <h2 class="header">Naturally Aspirated Vehicles</h2>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_1"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_2"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_3"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_4"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_5"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_6"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_7"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_8"></rule-input>
        <rule-input v-model="selectedRules" :rule="naRules.r6_7_9"></rule-input>
      </div>

      <div class="container">
        <h2 class="header">Wheels and Tires</h2>
        <div>Tire Warmers are prohibited.</div>
        <rule-input v-model="selectedRules" :rule="wheelTireRules.r6_8_1"></rule-input>
        <rule-input v-model="selectedRules" :rule="wheelTireRules.r6_8_2"></rule-input>
        <rule-input v-model="selectedRules" :rule="wheelTireRules.r6_8_3"></rule-input>
        <rule-input v-model="selectedRules" :rule="wheelTireRules.r6_8_4"></rule-input>
        <rule-input v-model="selectedRules" :rule="wheelTireRules.r6_8_5"></rule-input>
        <rule-input v-model="selectedRules" :rule="wheelTireRules.r6_8_6"></rule-input>
      </div>

      <div class="container">
        <h2 class="header">Your Selected Rules</h2>
        <div>selected rules: {{ selectedRules }}</div>
      </div>

    </div>


  </div>


</template>

<style>
.rulesSections {
  padding-bottom: 200px;
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

.pointsOverlay--bottom {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(255, 255, 255, 0.95);
  color: black;
  box-shadow: 0 -2px 8px rgba(0, 0, 0, 0.08);
  z-index: 1000;
  padding: 12px 24px;
  display: flex;
  justify-content: center;
  gap: 2rem;
  font-size: 1.2rem;
}
</style>
