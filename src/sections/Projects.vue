<template>
  <section id="projects" class="relative px-5 lg:px-28 py-32 overflow-hidden">
    <div class="absolute top-0 left-0 w-[500px] h-[500px] bg-cyan-500/5 rounded-full blur-[120px] -z-10"></div>
    <div class="absolute bottom-1/3 right-0 w-[400px] h-[400px] bg-[rgba(224,172,105,0.04)] rounded-full blur-[100px] -z-10"></div>

    <div class="mx-auto w-full max-w-7xl">
      <!-- Header -->
      <div class="mb-16 space-y-4 text-center lg:text-left">
        <span class="inline-block px-6 py-2 rounded-full bg-cyan-500/10 border border-cyan-500/20 text-cyan-400 text-xs font-black tracking-widest uppercase mb-4">
          Portfolio
        </span>
        <h2 class="text-5xl lg:text-8xl font-black tracking-tighter text-[var(--theme-text-strong)] uppercase leading-[0.9]">
          My <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">Projects</span>
        </h2>
      </div>

      <!-- Category Filter Tabs -->
      <div class="flex flex-wrap gap-3 mb-12">
        <button
          v-for="tab in tabs"
          :key="tab.key"
          @click="activeTab = tab.key"
          class="px-5 py-2.5 rounded-full text-sm font-bold tracking-wider uppercase transition-all duration-300 cursor-pointer border"
          :class="activeTab === tab.key
            ? 'bg-gradient-to-r from-cyan-500 to-blue-600 text-white border-transparent shadow-lg shadow-cyan-500/25'
            : 'bg-white/5 text-[var(--theme-text-muted)] border-white/10 hover:bg-white/10 hover:text-[var(--theme-text-strong)]'"
        >
          {{ tab.label }}
        </button>
      </div>

      <!-- Project Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div
          v-for="project in filteredProjects"
          :key="project.id"
          class="project-card group relative rounded-3xl overflow-hidden border border-white/10 bg-slate-900/60 backdrop-blur-xl transition-all duration-500 hover:-translate-y-3 hover:border-cyan-500/30"
        >
          <!-- Image Preview -->
          <div class="relative h-52 overflow-hidden bg-slate-800">
            <img
              :src="project.image"
              :alt="project.title"
              class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
              loading="lazy"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-slate-900 via-transparent to-transparent"></div>
            <span class="absolute top-4 left-4 px-3 py-1 rounded-full bg-black/60 backdrop-blur-sm text-[10px] font-black tracking-widest text-cyan-400 uppercase border border-cyan-500/20">
              {{ project.category }}
            </span>
          </div>

          <!-- Content -->
          <div class="p-6 space-y-4">
            <h3 class="text-xl font-black text-[var(--theme-text-strong)] group-hover:text-cyan-400 transition-colors leading-tight">
              {{ project.title }}
            </h3>
            <p class="text-sm text-[var(--theme-text-muted)] leading-relaxed font-['Oxanium'] line-clamp-3">
              {{ project.description }}
            </p>

            <!-- Tech tags -->
            <div class="flex flex-wrap gap-2">
              <span
                v-for="tag in project.tags"
                :key="tag"
                class="px-2.5 py-1 rounded-md bg-white/5 text-[10px] font-bold tracking-wider text-[var(--theme-text-soft)] uppercase border border-white/5"
              >
                {{ tag }}
              </span>
            </div>

            <!-- Action Buttons -->
            <div class="pt-2 flex items-center gap-3 flex-wrap">
              <a
                v-if="project.github"
                :href="project.github"
                target="_blank"
                rel="noopener noreferrer"
                class="action-btn"
              >
                <i class="bi bi-github"></i> Code
              </a>
              <a
                v-if="project.demo"
                :href="project.demo"
                target="_blank"
                rel="noopener noreferrer"
                class="action-btn action-btn--primary"
              >
                <i class="bi bi-box-arrow-up-right"></i> Live
              </a>
              <a
                v-if="project.youtube"
                :href="project.youtube"
                target="_blank"
                rel="noopener noreferrer"
                class="action-btn action-btn--youtube"
              >
                <i class="bi bi-youtube"></i> Demo
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue';
import progress1Img from '@/assets/progress1.jpg';

const activeTab = ref('all');

const tabs = [
  { key: 'all', label: 'All' },
  { key: 'fullstack', label: 'Full Stack' },
  { key: 'frontend', label: 'Frontend' },
  { key: 'clones', label: 'Clones' },
  { key: 'games', label: 'Games' },
];

const projects = [
  {
    id: 1,
    title: 'FixItNow',
    category: 'Full Stack',
    filterKey: 'fullstack',
    description: 'A full-stack local repair service booking platform connecting users with expert technicians for electronic and home appliance repairs. Built with MERN stack.',
    tags: ['React', 'Node.js', 'MongoDB', 'Express', 'Tailwind'],
    image: progress1Img,
    github: 'https://github.com/VIJAY33420',
    demo: '#', // TODO: Add your live demo URL
    youtube: '', // TODO: Add YouTube demo URL if available
  },
  {
    id: 2,
    title: 'Art Park AI Build',
    category: 'Full Stack',
    filterKey: 'fullstack',
    description: 'An intensive 48-hour hackathon project focused on building AI-driven solutions for real-world urban challenges at IISc Bangalore.',
    tags: ['React', 'Node.js', 'AI/ML', 'MongoDB'],
    image: progress1Img,
    github: 'https://github.com/VIJAY33420',
    demo: '',
    youtube: '',
  },
  {
    id: 3,
    title: 'Portfolio Website',
    category: 'Frontend',
    filterKey: 'frontend',
    description: 'A premium personal portfolio built with Vue 3, Tailwind CSS, and GSAP featuring glassmorphic design, dark/light theme, and smooth scroll animations.',
    tags: ['Vue 3', 'Tailwind', 'GSAP', 'Vite'],
    image: progress1Img,
    github: 'https://github.com/VIJAY33420/vijay-portfolio',
    demo: 'https://vijaydiwaniya-portfolio.vercel.app/',
    youtube: '',
  },
  {
    id: 4,
    title: 'Netflix Clone',
    category: 'Clones',
    filterKey: 'clones',
    description: 'A pixel-perfect Netflix UI clone featuring responsive design, dynamic content sections, and smooth hover animations.',
    tags: ['HTML', 'CSS', 'JavaScript'],
    image: progress1Img,
    github: 'https://github.com/VIJAY33420', // TODO: Update with actual repo
    demo: '', // TODO: Add live demo URL
    youtube: '',
  },
  {
    id: 5,
    title: 'Tic-Tac-Toe',
    category: 'Games',
    filterKey: 'games',
    description: 'An interactive Tic-Tac-Toe game with clean UI, win detection logic, score tracking, and responsive design.',
    tags: ['HTML', 'CSS', 'JavaScript'],
    image: progress1Img,
    github: 'https://github.com/VIJAY33420', // TODO: Update with actual repo
    demo: '', // TODO: Add live demo URL
    youtube: '',
  },
  {
    id: 6,
    title: 'Weather App',
    category: 'Frontend',
    filterKey: 'frontend',
    description: 'A real-time weather application fetching live data from OpenWeatherMap API with beautiful UI and location search.',
    tags: ['React', 'API', 'CSS', 'Axios'],
    image: progress1Img,
    github: 'https://github.com/VIJAY33420', // TODO: Update with actual repo
    demo: '', // TODO: Add live demo URL
    youtube: '',
  },
];

const filteredProjects = computed(() => {
  if (activeTab.value === 'all') return projects;
  return projects.filter(p => p.filterKey === activeTab.value);
});
</script>

<style scoped>
.project-card {
  box-shadow: 0 20px 60px -20px rgba(0, 0, 0, 0.5);
}

.project-card:hover {
  box-shadow: 0 30px 70px -20px rgba(6, 182, 212, 0.15), 0 20px 60px -20px rgba(0, 0, 0, 0.6);
}

.action-btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 16px;
  border-radius: 10px;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: var(--theme-text-soft);
  transition: all 0.25s ease;
  text-decoration: none;
}

.action-btn:hover {
  background: rgba(255, 255, 255, 0.1);
  color: var(--theme-text-strong);
  transform: translateY(-1px);
}

.action-btn--primary {
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.2), rgba(59, 130, 246, 0.2));
  border-color: rgba(6, 182, 212, 0.3);
  color: #22d3ee;
}

.action-btn--primary:hover {
  background: linear-gradient(135deg, rgba(6, 182, 212, 0.4), rgba(59, 130, 246, 0.4));
  box-shadow: 0 4px 16px rgba(6, 182, 212, 0.2);
}

.action-btn--youtube {
  background: rgba(255, 0, 0, 0.1);
  border-color: rgba(255, 0, 0, 0.2);
  color: #ef4444;
}

.action-btn--youtube:hover {
  background: rgba(255, 0, 0, 0.2);
  box-shadow: 0 4px 16px rgba(255, 0, 0, 0.15);
}

.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

:global([data-theme="light"]) .project-card {
  background: rgba(255, 255, 255, 0.8);
  border-color: rgba(0, 0, 0, 0.08);
}

:global([data-theme="light"]) .project-card:hover {
  box-shadow: 0 20px 60px -20px rgba(6, 182, 212, 0.1), 0 10px 30px -10px rgba(0, 0, 0, 0.1);
}

:global([data-theme="light"]) .action-btn {
  background: rgba(0, 0, 0, 0.04);
  border-color: rgba(0, 0, 0, 0.1);
  color: var(--theme-text-muted);
}
</style>
