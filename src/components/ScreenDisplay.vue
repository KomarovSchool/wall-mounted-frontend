<template>
  <div>
    <SlideShow v-if="data?.type === 'slides'" :images="data.images" />
    <p v-else>Invalid data type</p>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import SlideShow from './SlideShow.vue';

const route = useRoute();
const data = ref(null);

onMounted(async () => {
  try {
    const response = await fetch(`/api/data/${route.params.intId}`);
    data.value = await response.json();
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>
