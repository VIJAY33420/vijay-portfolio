<template>
  <div class="custom-cursor-container" :class="{ 'is-active': isActive }" aria-hidden="true">
    <!-- The main glowing pointer -->
    <div ref="cursorPointer" class="cursor-pointer-wrapper">
      <div class="glow-layer pink-glow"></div>
      <div class="glow-layer blue-glow"></div>
      <div class="main-pointer"></div>
    </div>
    <!-- The lagging outer ring -->
    <div ref="cursorRing" class="cursor-ring"></div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';
import gsap from 'gsap';

const cursorPointer = ref(null);
const cursorRing = ref(null);
const isActive = ref(false);

let xToPointer, yToPointer, xToRing, yToRing;

const onMouseMove = (e) => {
  if (!isActive.value) isActive.value = true;
  
  const { clientX, clientY } = e;
  
  xToPointer(clientX);
  yToPointer(clientY);
  xToRing(clientX);
  yToRing(clientY);
};

const onMouseEnter = () => {
  gsap.to([cursorPointer.value, cursorRing.value], {
    opacity: 1,
    duration: 0.3,
  });
};

const onMouseLeave = () => {
  gsap.to([cursorPointer.value, cursorRing.value], {
    opacity: 0,
    duration: 0.3,
  });
};

const onHoverStart = () => {
  gsap.to(cursorPointer.value, {
    scale: 1.5,
    duration: 0.3,
    ease: "back.out(1.7)"
  });
  gsap.to(cursorRing.value, {
    scale: 2,
    opacity: 0.2,
    duration: 0.3,
  });
};

const onHoverEnd = () => {
  gsap.to(cursorPointer.value, {
    scale: 1,
    duration: 0.3,
    ease: "power2.out"
  });
  gsap.to(cursorRing.value, {
    scale: 1,
    opacity: 1,
    duration: 0.3,
  });
};

onMounted(() => {
  if (window.matchMedia('(pointer: coarse)').matches) return;

  // Quick setters for smooth follow
  xToPointer = gsap.quickTo(cursorPointer.value, "x", { duration: 0.05, ease: "none" });
  yToPointer = gsap.quickTo(cursorPointer.value, "y", { duration: 0.05, ease: "none" });
  xToRing = gsap.quickTo(cursorRing.value, "x", { duration: 0.35, ease: "power3.out" });
  yToRing = gsap.quickTo(cursorRing.value, "y", { duration: 0.35, ease: "power3.out" });

  window.addEventListener('mousemove', onMouseMove);
  document.addEventListener('mouseenter', onMouseEnter);
  document.addEventListener('mouseleave', onMouseLeave);

  const addHoverListeners = () => {
    const targets = document.querySelectorAll('a, button, [role="button"], input, textarea, .cursor-pointer');
    targets.forEach(target => {
      target.addEventListener('mouseenter', onHoverStart);
      target.addEventListener('mouseleave', onHoverEnd);
    });
  };

  addHoverListeners();
  const observer = new MutationObserver(addHoverListeners);
  observer.observe(document.body, { childList: true, subtree: true });

  onUnmounted(() => {
    window.removeEventListener('mousemove', onMouseMove);
    document.removeEventListener('mouseenter', onMouseEnter);
    document.removeEventListener('mouseleave', onMouseLeave);
    observer.disconnect();
  });
});
</script>

<style scoped>
.custom-cursor-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 10000;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.custom-cursor-container.is-active {
  opacity: 1;
}

.cursor-pointer-wrapper {
  position: absolute;
  width: 20px;
  height: 20px;
  top: 0;
  left: 0;
  transform: translate(-5px, -5px); /* Offset slightly for tip alignment */
  z-index: 10002;
}

.main-pointer {
  position: absolute;
  width: 0;
  height: 0;
  border-left: 7px solid transparent;
  border-right: 7px solid transparent;
  border-bottom: 16px solid white;
  transform: rotate(-30deg); /* Classic cursor angle */
}

.glow-layer {
  position: absolute;
  inset: 0;
  width: 0;
  height: 0;
  border-left: 8px solid transparent;
  border-right: 8px solid transparent;
  transform: rotate(-30deg);
  filter: blur(4px);
  opacity: 0.8;
}

.pink-glow {
  border-bottom: 18px solid #ff2d75;
  transform: rotate(-30deg) translate(-1.5px, -1px);
}

.blue-glow {
  border-bottom: 18px solid #00d2ff;
  transform: rotate(-30deg) translate(1.5px, 1px);
}

.cursor-ring {
  position: absolute;
  top: -20px;
  left: -20px;
  width: 40px;
  height: 40px;
  border: 1px solid rgba(224, 172, 105, 0.15);
  border-radius: 50%;
  z-index: 10001;
}

/* Hide native cursor */
@media (pointer: fine) {
  :global(body), :global(a), :global(button), :global(.cursor-pointer) {
    cursor: none !important;
  }
}
</style>
