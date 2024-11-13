<script setup>
import {ref, watch, onMounted, computed} from 'vue'
const waterOz = ref(6)
const waxOz = ref(5)
const fLoad = ref(6)
const endFOz = computed(()=> waxOz.value - (waxOz.value / (  1 + ( fLoad.value / 100 ))))
const endWaxOz = computed(()=> waxOz.value / (  1 + ( fLoad.value / 100 )) )
onMounted(updateWax)

function updateWax(){
  waxOz.value = (waterOz.value * .86)
}
function updateWater(){
  waterOz.value = (waxOz.value / .86)
}
</script>


<template>
  <main data-bs-theme="dark" class="container">
    <form class="row g-4">
      <div class="col">
        <div class="mb-2">
          <label for="">water in oz</label>
          <input @input="updateWax" v-model="waterOz" type="number" class="form-control">
        </div>
        <div class="mb-2">
          <label for="">wax in oz</label>
          <input @input="updateWater" v-model="waxOz" type="number" class="form-control">
        </div>
      </div>
      <div class="col">
        <div class="mb-2">
          <label for="">Fragrance load {{ fLoad }}%</label>
          <input v-model="fLoad" type="range" class="form-range" min="2" max="15">
        </div>
      </div>
    </form>
    <hr>
    <section class="text-center my-2">
      Yields
    </section>
    <section class="d-flex justify-content-around fs-4">
      <div class="text-indigo"><i class="mdi mdi-dots-hexagon"></i>{{ endWaxOz.toFixed(2) }}oz  wax</div>
        <div class="text-blue"><i class="mdi mdi-water"></i>{{ endFOz.toFixed(2) }}oz fragrance</div>
    </section>
  </main>
</template>

<style scoped>

</style>
