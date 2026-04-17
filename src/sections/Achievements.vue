<template>
  <section id="achievements" class="relative px-5 lg:px-28 py-32 overflow-hidden bg-[var(--theme-bg)]">
    <!-- Background Accents -->
    <div class="absolute top-1/2 left-0 w-[400px] h-[400px] bg-cyan-500/5 rounded-full blur-[100px] -z-10 animate-pulse"></div>

    <div class="mx-auto w-full max-w-7xl">
      <div class="mb-20 space-y-4 text-center lg:text-left">
        <span class="inline-block px-4 py-1.5 rounded-full bg-cyan-500/10 border border-cyan-500/20 text-cyan-400 text-xs font-black tracking-widest uppercase mb-4">
          Milestones
        </span>
        <h2 class="text-5xl lg:text-7xl font-black tracking-tighter text-[var(--theme-text-strong)] uppercase leading-[0.9]">
          Key <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">Achievements</span>
        </h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div 
          v-for="(achievement, index) in achievements" 
          :key="index"
          class="achievement-card group relative p-px rounded-3xl bg-gradient-to-br from-white/10 to-transparent hover:from-cyan-500/30 transition-all duration-500"
        >
          <div class="relative h-full p-8 rounded-[23px] bg-slate-900/80 backdrop-blur-xl flex gap-6 items-start overflow-hidden">
            <!-- Icon/Badge -->
            <div class="flex-shrink-0 w-16 h-16 rounded-2xl bg-cyan-500/10 border border-cyan-500/20 flex items-center justify-center text-cyan-400 shadow-lg group-hover:scale-110 transition-transform duration-500">
              <i :class="achievement.icon" class="text-3xl"></i>
            </div>

            <div class="space-y-3">
              <div class="flex items-center gap-3">
                <span class="text-[10px] font-black tracking-widest text-cyan-500/70 uppercase">{{ achievement.category }}</span>
                <span class="text-[10px] text-[var(--theme-text-muted)] font-bold">{{ achievement.date }}</span>
              </div>
              <h3 class="text-xl font-black text-[var(--theme-text-strong)] group-hover:text-cyan-400 transition-colors">
                {{ achievement.title }}
              </h3>
              <p class="text-sm text-[var(--theme-text-muted)] leading-relaxed font-['Oxanium']">
                {{ achievement.description }}
              </p>
            </div>
            
            <!-- Decorative circle -->
            <div class="absolute -right-10 -bottom-10 w-32 h-32 bg-cyan-500/5 rounded-full blur-3xl group-hover:bg-cyan-500/10 transition-colors"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';

const achievements = ref([
  {
    title: "Art Park AI Build Hackathon Winner",
    category: "Competition",
    date: "2024",
    icon: "bi bi-trophy-fill",
    description: "Secured a top position among national teams by building an innovative AI-driven prototype for urban development challenge."
  },
  {
    title: "100+ LeetCode Problems Solved",
    category: "Coding",
    date: "Ongoing",
    icon: "bi bi-code-slash",
    description: "Consistently tackling complex algorithmic challenges to strengthen data structures and logic expertise."
  },
  {
    title: "Certified MERN Stack Specialist",
    category: "Professional",
    date: "2024",
    icon: "bi bi-patch-check-fill",
    description: "Completed rigorous full-stack training with hands-on projects in React, Node.js, and MongoDB."
  },
  {
    title: "B.Tech CSE Academic Excellence",
    category: "Academic",
    date: "2021 - 2025",
    icon: "bi bi-mortarboard-fill",
    description: "Maintaining a high CGPA while actively participating in technical societies and innovation labs."
  }
]);
</script>

<style scoped>
.achievement-card {
  box-shadow: 0 20px 40px -20px rgba(0, 0, 0, 0.5);
}
</style>
