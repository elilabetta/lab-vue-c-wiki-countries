<script setup>
import {ref, computed, watch} from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute();

const country = ref(null)

const countryCode = computed(() => {
  return route.params.alpha3Code;
})

const getCountryByAlphaCode = async () => {
  const alpha3Code = route.params.alpha3Code;
  
  const response = await fetch(`https://ih-countries-api.herokuapp.com/countries/${alpha3Code}`)

  const finalResponse = await response.json();

  country.value = finalResponse;
}
getCountryByAlphaCode();

watch(countryCode, (newCountryCode) => {
  getCountryByAlphaCode();
})
</script>

<template>
  <section v-if="country">
    <h1>{{country.name.common}}</h1>
  </section>
</template>
  

  
  <style scoped>
  
  </style>