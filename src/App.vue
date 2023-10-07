<script setup>
//Computed (propiedades computadas o calculadas)

import { ref, computed } from "vue";

const name = "Vue dinámico";

const counter = ref(0);

const increment = () => {
  counter.value++;
}

const decrement = () => {
  counter.value--;
}

const reset = () => {
  counter.value = 0;
}

const numerosFavoritos = ref([]);

//Se pudo haber obtenido el mismo resultado con una función o método, pero con datos que son reactivos, se recomienda utilizar el computed
const classCounter = computed(() => {

  if(counter.value === 0){
    return 'zero';
  }

  if(counter.value > 0){
    return 'positive';
  }

  if(counter.value < 0){
    return 'negative';
  }
})

const addFav = () => {
  numerosFavoritos.value.push(counter.value);
}

const bloquearBtnAdd = computed(() => {
  const numSearch = numerosFavoritos.value.find((num) => num === counter.value);
  console.log(numSearch);
  //MANERA LARGA:
  if (numSearch === 0) return true;
  return numSearch ? true : false;
  //MANERA SIMPLE:
  return numSearch || numSearch === 0
  //LO ANTERIOR ES QUE numSearch puede devolver true o false, y numSearch va devolver true
});

</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Restablecer</button>
      <button @click="addFav" :disabled="bloquearBtnAdd" class="btn btn-primary">Agregar a Favoritos</button>
    </div>

    <h1>Números favoritos</h1>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="(num, index) in numerosFavoritos" :key="index">{{ num }}</li>
    </ul>
  </div>  
</template>

<style>
  h1 {
    color: blueviolet;
  }

  .positive {
    color: green;
  }

  .negative {
    color: red;
  }

  .zero {
    color: black;
  }
</style>