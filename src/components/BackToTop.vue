<template>
  <Teleport to="body">
    <button
      v-show="isVisible"
      class="back-to-top"
      :class="{ 'is-visible': isVisible }"
      @click="scrollToTop"
      aria-label="Back to top"
    >
      <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
        <polyline points="18 15 12 9 6 15"></polyline>
      </svg>
    </button>
  </Teleport>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const isVisible = ref(false);

const handleScroll = () => {
  isVisible.value = window.scrollY > 600;
};

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true });
});

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
.back-to-top {
  position: fixed;
  bottom: 2rem;
  left: 2rem;
  z-index: 90;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(224, 172, 105, 0.9), rgba(141, 91, 76, 0.9));
  border: 1px solid rgba(255, 255, 255, 0.15);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 0 8px 24px rgba(224, 172, 105, 0.3);
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.3s ease, transform 0.3s ease, background 0.2s ease;
}

.back-to-top.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.back-to-top:hover {
  background: linear-gradient(135deg, rgba(224, 172, 105, 1), rgba(141, 91, 76, 1));
  transform: translateY(-3px);
  box-shadow: 0 12px 32px rgba(224, 172, 105, 0.4);
}
</style>
