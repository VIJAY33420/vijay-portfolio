<template>
  <Teleport to="body">
    <div
      v-if="visible"
      class="resume-modal-backdrop"
      @click.self="$emit('close')"
      @keydown.escape="$emit('close')"
    >
      <div class="resume-modal-container" role="dialog" aria-modal="true" aria-label="Resume Viewer">
        <button
          class="resume-modal-close"
          @click="$emit('close')"
          aria-label="Close resume viewer"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>
        <iframe
          :src="resumeUrl"
          class="resume-modal-iframe"
          title="Resume PDF"
          allow="fullscreen"
        ></iframe>
      </div>
    </div>
  </Teleport>
</template>

<script setup>
defineProps({
  visible: { type: Boolean, default: false },
  resumeUrl: { type: String, default: '/resume/resume-en.pdf' }
});
defineEmits(['close']);
</script>

<style scoped>
.resume-modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 200;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.85);
  backdrop-filter: blur(12px);
  animation: resumeFadeIn 0.3s ease;
}

.resume-modal-container {
  position: relative;
  width: 90vw;
  height: 90vh;
  max-width: 900px;
  border-radius: 20px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 40px 80px rgba(0, 0, 0, 0.6);
  animation: resumeSlideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.resume-modal-close {
  position: absolute;
  top: 16px;
  right: 16px;
  z-index: 10;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.7);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.2s, transform 0.2s;
}

.resume-modal-close:hover {
  background: rgba(224, 172, 105, 0.8);
  transform: scale(1.1);
}

.resume-modal-iframe {
  width: 100%;
  height: 100%;
  border: none;
  background: white;
}

@keyframes resumeFadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes resumeSlideUp {
  from { opacity: 0; transform: translateY(40px) scale(0.95); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}
</style>
