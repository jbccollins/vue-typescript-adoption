<script setup lang="ts">
interface Props {
  count: number
}
const props = defineProps<Props>()

// Intentionally misspelled variable for demonstration
const doubled = props.count * 2 // Error: Property 'cout' does not exist on type 'Props'
</script>

<template>
  <div>
    <p>Original: {{ props.count }}</p>
    <p>Doubled: {{ doubled }}</p>
  </div>
</template>
