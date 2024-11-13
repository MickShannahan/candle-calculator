<script setup>
import {ref, watch, onMounted, computed} from 'vue'
const waxLb = ref(1)
const waxOz = ref(0)
const fLoad = ref(6)
const endWaxOz = computed(()=> waxOz.value - (waxOz.value*(fLoad.value / 100)))
const endFOz = computed(()=> waxOz.value * (fLoad.value / 100) )
onMounted(updateOz)

function updateOz(){
  waxOz.value = waxLb.value * 16
}
function updateLb(){
  waxLb.value = waxOz.value / 16
}
</script>


<template>
  <main data-bs-theme="dark" class="container">
    <form class="row g-4">
      <div class="col">
        <div class="mb-2">
          <label for="">wax in pounds</label>
          <input @change="updateOz" v-model="waxLb" type="number" class="form-control">
        </div>
        <div class="mb-2">
          <label for="">wax in oz</label>
          <input @change="updateLb" v-model="waxOz" type="number" class="form-control">
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
    <section class="d-flex justify-content-between">
      <div>
        <div>
          {{ waxOz }} <i class="mdi mdi-multiplication"></i> 0.{{ fLoad }} = {{ waxOz * (fLoad / 100) }}
        </div>
        <div>
          {{waxOz}} - {{ waxOz * (fLoad / 100) }} = {{endWaxOz}}
        </div>
      </div>
      <div class="text-blue fs-5">
        <div><i class="mdi mdi-water"></i>{{ endFOz.toFixed(2) }}oz of fragrance</div>
        <div class="text-indigo"><i class="mdi mdi-dots-hexagon"></i>{{ endWaxOz.toFixed(2) }}oz of wax</div>
      </div>
    </section>
  </main>
</template>

<style scoped>

</style>
