<script setup>
// defineProps(['title']);
// const props = defineProps(['title'])
// console.log(props.title)
// String, Number, Boolean, Array, Object, Date, Function, Symbol
// esta va en el parte de button abajo del class @click="$emit('fijarFavorito', title)"
defineProps({
  title: String,
  id: Number,
  body: {
      type: String,
      default: 'Sin descripción'
  },
  fijarFavorito: Function,
});

const emit = defineEmits(["fijarFavorito"]);
</script>

<template>
  <!-- <h2>{{ title }}</h2> -->
  <!-- <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ id }} - {{ title }}</h5>
      <p>{{ body }}</p>
      <button
        class="btn btn-sm btn-outline-primary"
        @click="fijarFavorito(title)"
        >
            Mi Favorito
      </button>
    </div>
  </div> -->
  <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p>{{ body }}</p>
            <button
                class="btn btn-sm btn-outline-primary"
                @click="$emit('fijarFavorito', title)"
            >
                Mi Favorito
            </button>
        </div>
    </div>
</template>