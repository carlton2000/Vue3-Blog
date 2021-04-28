<template>
  <div class="home">
<h3>Serarch the Word</h3>
<input type="text" v-model="search">
<p>search term : {{ search }}</p>
<div v-for="name in matchingNames" :key="name">
  <p>{{ name }}</p>
</div>
  <button @click="handleClick">stop watching</button>
  </div>
</template>

<script>
import {computed, ref, watch, watchEffect } from 'vue'

export default {
  name: 'Home',
  setup() {
     const search = ref('')
     const names = ref(['carl', 'visa', 'carlito', 'vista'])

     const stopwatch = watch(search, () => {
       console.log('watch function ran', search.value)
     })

      const stopEffect = watchEffect(() => {
       console.log('watchEffect function ran', search.value)
     })

     const matchingNames = computed(() => {
       return names.value.filter((name) => name.includes(search.value))
     })

     const handleClick = () => {
        stopwatch()
        stopEffect()
     }

     return { names, search, matchingNames, handleClick }

  }
}
</script>

