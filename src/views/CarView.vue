<script setup>
import { useRouter, useRoute, RouterView } from "vue-router";
import { ref, onBeforeMount } from "vue";
import cars from "../data.json";

const car = ref(null);
const route = useRoute();
const router = useRouter();

const { id } = route.params;

onBeforeMount(() => {
  car.value = cars.find((c) => c.id === +id);
});
</script>

<template>
  <div class="container">
    <div v-if="car">
      <button @click="router.push({ name: 'home' })">Go Back</button>
      <button @click="router.replace(`/car/${id}/manufacture`)">
        Manufacture
      </button>
      <button @click="router.replace(`/car/${id}/dealer`)">Dealer</button>
      <h1>The car</h1>
      <p>Make: {{ car.make }}</p>
      <p>Body: {{ car.body }}</p>
      <p>Price: {{ car.price }}</p>
      <p>Year: {{ car.year }}</p>
      <!-- Children Routes -->
      <RouterView />
    </div>
    <div v-else>
      <h1>Car Not Found!!</h1>
    </div>
  </div>
</template>
