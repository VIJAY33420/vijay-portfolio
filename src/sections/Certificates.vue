<template>
  <section id="certificates" class="relative px-5 lg:px-28 py-32 overflow-hidden">
    <!-- Decorative background elements -->
    <div class="absolute top-0 right-0 w-[500px] h-[500px] bg-[rgba(224,172,105,0.03)] rounded-full blur-[120px] -z-10"></div>
    <div class="absolute bottom-0 left-0 w-[500px] h-[500px] bg-[rgba(24,150,158,0.03)] rounded-full blur-[120px] -z-10"></div>

    <div class="mx-auto w-full max-w-7xl">
      <div class="mb-24 space-y-6 text-center lg:text-left">
        <span class="inline-block px-8 py-3 rounded-full bg-[rgba(224,172,105,0.08)] border border-[rgba(224,172,105,0.25)] text-[#E0AC69] text-sm font-black tracking-[0.4em] uppercase mb-4 shadow-[0_0_20px_rgba(224,172,105,0.1)]">
          Credentials
        </span>
        <h2 class="text-6xl lg:text-9xl font-black tracking-tighter text-[var(--theme-text-strong)] leading-[0.85] uppercase">
          Certification<br/><span class="text-transparent bg-clip-text bg-gradient-to-r from-[#E0AC69] to-[#D4A017]">& Success</span>
        </h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
        <div 
          v-for="(cert, index) in certificates" 
          :key="index"
          class="cert-card group relative p-1 rounded-3xl transition-all duration-700 hover:-translate-y-4"
        >
          <!-- Neon border glow effect -->
          <div class="absolute inset-0 bg-gradient-to-br from-[#E0AC69] via-transparent to-[#18969E] opacity-20 rounded-3xl blur-sm group-hover:opacity-60 transition-opacity duration-700"></div>
          
          <div class="relative h-full p-8 rounded-[22px] bg-[rgba(10,15,25,0.8)] backdrop-blur-xl border border-white/5 flex flex-col justify-between overflow-hidden">
            <!-- Background pattern -->
            <div class="absolute -right-4 -top-4 text-white/[0.02] font-black text-8xl italic pointer-events-none select-none">
              {{ index + 1 }}
            </div>

            <div class="space-y-8 relative z-10">
              <div class="flex justify-between items-center">
                <div class="w-14 h-14 rounded-2xl bg-gradient-to-br from-[rgba(224,172,105,0.2)] to-transparent border border-[rgba(224,172,105,0.3)] flex items-center justify-center text-[#E0AC69] shadow-[0_0_20px_rgba(224,172,105,0.1)]">
                  <svg xmlns="http://www.w3.org/2000/svg" class="w-7 h-7" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M22 10v6M2 10l10-5 10 5-10 5z"/>
                    <path d="M6 12v5c3 3 9 3 12 0v-5"/>
                  </svg>
                </div>
                <div class="px-4 py-1 rounded-full bg-white/5 border border-white/10 text-[10px] font-black tracking-widest text-[#E0AC69] uppercase">
                  {{ cert.issuer }}
                </div>
              </div>

              <div class="space-y-3">
                <h3 class="text-2xl font-black text-[var(--theme-text-strong)] leading-tight tracking-tight">
                  {{ cert.title }}
                </h3>
                <p class="text-[15px] text-[var(--theme-text-muted)] leading-relaxed font-light font-['Oxanium'] group-hover:text-[var(--theme-text-soft)] transition-colors duration-500">
                  {{ cert.description }}
                </p>
              </div>
            </div>

            <div class="pt-10 flex items-center justify-between relative z-10">
              <div class="flex flex-col">
                <span class="text-[10px] font-bold text-[var(--theme-text-muted)] uppercase tracking-widest">Issued</span>
                <span class="text-sm font-black text-[var(--theme-text-strong)]">{{ cert.date }}</span>
              </div>
              <a :href="cert.link" target="_blank" class="group/btn flex items-center gap-3 px-6 py-3 rounded-xl bg-white/5 border border-white/10 text-xs font-black tracking-widest uppercase text-white hover:bg-[#E0AC69] hover:text-black hover:border-transparent transition-all duration-300">
                Verify
                <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 transition-transform group-hover/btn:translate-x-1" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
                  <line x1="5" y1="12" x2="19" y2="12"></line>
                  <polyline points="12 5 19 12 12 19"></polyline>
                </svg>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();

const certificates = ref([
  {
    title: "ArtPark CodeForge Hackathon",
    issuer: "IISc, Bangalore",
    date: "2024",
    link: "/certs/cert-iisc.jpg",
    description: "Participated as Team Debugger in the Prototype Development Round, building innovative solutions for real-world urban challenges."
  },
  {
    title: "Neural Nexus (IIT Jammu)",
    issuer: "IIT Jammu",
    date: "2024",
    link: "/certs/cert-iitjammu.jpg",
    description: "Participation certificate for the ‘Neural Nexus’ event organized by IIT Jammu, representing Swaminarayan University as Team DeBugger."
  },
  {
    title: "MERN Stack Specialist",
    issuer: "Coursera / Meta",
    date: "2024",
    link: "#",
    description: "Advanced certification focusing on building scalable full-stack applications using MongoDB, Express, React, and Node.js."
  }
]);
</script>

<style scoped>
.cert-card {
  box-shadow: 0 10px 30px -15px rgba(0, 0, 0, 0.3);
}

:root[data-theme="light"] .cert-card {
  background: white;
  box-shadow: 0 10px 30px -15px rgba(15, 23, 42, 0.1);
}
</style>
