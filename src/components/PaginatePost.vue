<script setup>
defineProps(['inicio','fin','maxLength'])
const emit = defineEmits(['nextPage','previousPage'])

</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button type="button"
            @click="emit('previousPage')"
            class="btn btn-outline-light"
            :disabled="inicio === 0">Prev.</button>
    <button type="button"
            @click="emit('nextPage')"
            class="btn btn-outline-light"
            :disabled="fin >= maxLength">Next</button>
  </div>
</template>
