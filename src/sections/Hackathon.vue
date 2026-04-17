<template>
  <section id="hackathon" class="relative px-5 lg:px-28 py-24 overflow-hidden">
    <!-- Decorative background elements -->
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[500px] h-[500px] bg-[rgba(224,172,105,0.03)] blur-[120px] rounded-full pointer-events-none"></div>

    <div class="mx-auto w-full max-w-6xl relative z-10">
      <div 
        ref="contentEl"
        class="hackathon-card transition-all duration-1000"
        :class="isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-12'"
      >
        <div class="flex flex-col lg:flex-row gap-12 items-center">
          <div class="lg:w-1/2 space-y-8">
            <div class="space-y-4">
              <span class="inline-block px-8 py-3 rounded-full bg-[rgba(224,172,105,0.08)] border border-[rgba(224,172,105,0.25)] text-[#E0AC69] text-sm lg:text-base font-black tracking-[0.4em] uppercase mb-4 shadow-[0_0_20px_rgba(224,172,105,0.1)]">
                Hackathon Experience
              </span>
            <h2 class="text-5xl lg:text-8xl font-black tracking-tighter text-[var(--theme-text-strong)] leading-[0.9] uppercase">
                Art Park AI Build <br/>
                <span class="text-[var(--theme-text-muted)] font-thin italic lowercase tracking-tight">48-Hour Sprint</span>
              </h2>
            </div>
            
            <p class="text-lg lg:text-xl text-[var(--theme-text-muted)] leading-relaxed font-light font-['Oxanium']">
              Participated in an intensive hackathon focused on building AI-driven solutions for real-world urban challenges. 
              Worked in a fast-paced environment to design, develop, and present a functional prototype within 48 hours.
            </p>

            <div class="flex flex-wrap gap-4">
              <span v-for="tag in ['AI/ML', 'Next.js', 'FastAPI', 'Urban Tech']" :key="tag" class="px-3 py-1 text-sm border border-[var(--theme-line-soft)] text-[var(--theme-text-muted)] font-medium">
                {{ tag }}
              </span>
            </div>
          </div>

          <div class="lg:w-1/2 relative group">
            <div class="absolute -inset-4 bg-gradient-to-r from-[#E0AC69]/10 to-[#8D5B4C]/10 blur-2xl opacity-0 group-hover:opacity-100 transition-opacity duration-700"></div>
            <div class="hackathon-visual relative aspect-video w-full rounded-2xl border border-[rgba(224,172,105,0.15)] bg-[rgba(255,255,255,0.02)] backdrop-blur-sm flex items-center justify-center overflow-hidden">
               <div class="absolute inset-0 bg-gradient-to-br from-[rgba(224,172,105,0.05)] to-transparent"></div>
               <div class="relative flex flex-col items-center gap-4 text-center p-8">
                 <div class="w-20 h-20 rounded-full border-2 border-[#E0AC69]/30 flex items-center justify-center animate-pulse">
                   <svg xmlns="http://www.w3.org/2000/svg" class="w-10 h-10 text-[#E0AC69]" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                     <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
                   </svg>
                 </div>
                 <div>
                   <span class="block text-[#E0AC69] font-bold text-lg mb-1">AI SOLUTIONS</span>
                   <span class="text-[var(--theme-text-soft)] text-sm tracking-widest uppercase">Urban Challenge Prototype</span>
                 </div>
               </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const contentEl = ref(null);
const isVisible = ref(false);
let observer = null;

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      isVisible.value = entry.isIntersecting;
    });
  }, { threshold: 0.2 });

  if (contentEl.value) observer.observe(contentEl.value);
});

onUnmounted(() => {
  if (observer) observer.disconnect();
});
</script>

<style scoped>
.hackathon-card {
  will-change: transform, opacity;
}

.hackathon-visual {
  transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

.hackathon-card:hover .hackathon-visual {
  transform: translateY(-8px) scale(1.01);
}
</style>
