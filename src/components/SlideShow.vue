<template>
  <div class="slideshow">
    <transition name="fade" mode="out-in">
      <img :key="currentIndex" :src="images[currentIndex]" alt="Slideshow Image" />
    </transition>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

defineProps<{
  images: string[];
}>();

const currentIndex = ref(0);

const nextImage = () => {
  currentIndex.value = (currentIndex.value + 1) % images.length;
};

onMounted(() => {
  setInterval(nextImage, 3000);
});
</script>

<style>
.slideshow {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

img {
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 1s ease-in-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
