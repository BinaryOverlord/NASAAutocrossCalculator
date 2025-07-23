<script setup lang="ts">
import type { Rule } from '../Logic/Rule'

    const model = defineModel();
const props = defineProps<{rule: Rule}>()

</script>

<template>
     <div class="rule">
        <div>{{ props.rule.description }}</div>
        <div>{{ props.rule.points }}</div>
        <div>
          <input type="checkbox" :value="props.rule.refNumer" v-model="model" />
        </div>
      </div>
</template>