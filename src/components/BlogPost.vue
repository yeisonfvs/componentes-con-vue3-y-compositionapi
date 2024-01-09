<script setup>
// const props = defineProps(["title","id","body", "colorText"]);
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: 'sin descripcion',
  },
  colorText: String,
});

const emit = defineEmits(['cambiarFavoritoNombre']);
// emit('cambiarFavoritoNombre', title)
</script>

<template>
  <div class="card m-3">
    <div class="card-body">
      <h5 class="card-title" :class="`text-${colorText}`">
        {{ id }} . {{ title }}
      </h5>
      <p>{{ body }}</p>
      <button
        @click="emit('cambiarFavoritoNombre', id)"
        class="btn btn-outline-primary"
      >
        Favorito
      </button>
    </div>
  </div>
</template>

<style></style>
