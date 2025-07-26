<script setup lang="ts">
import type { Rule } from '../Logic/Rule'

    const model = defineModel();
const props = defineProps<{rule: Rule}>()

</script>

<template>
     <div class="rule">
       <div>
          <input type="checkbox" :value="props.rule.refNumer" v-model="model" />
        </div>
        <div>{{ props.rule.points }}</div>
        <div>{{ props.rule.description }}</div>
      </div>
</template>
