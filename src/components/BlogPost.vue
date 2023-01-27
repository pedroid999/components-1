<script setup>

  defineProps({
    title: String,
    id: Number,
    body:{
      type: String,
      default: "Sin descripción",
    }
  })

  const emit = defineEmits(['cambiarFavoritoNombre'])

</script>

<template>
    <div class="card">
      <div class="card-body">
        <h5 class="text-dark">
          {{ id }} - {{ title }}
        </h5>
        <p class="text-dark">{{ body }}</p>
        <button class="btn btn-outline-primary" @click="emit('cambiarFavoritoNombre', title)">Favorito</button>
      </div>
    </div>
</template>

