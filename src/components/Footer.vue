<template>
  <footer class="relative px-5 lg:px-28 py-16 border-t border-white/5">
    <div class="mx-auto w-full max-w-7xl">
      <!-- Social Links Grid -->
      <div class="flex flex-wrap justify-center gap-4 mb-12">
        <a
          v-for="social in socials"
          :key="social.name"
          :href="social.url"
          target="_blank"
          rel="noopener noreferrer"
          class="footer-social group"
          :title="social.name"
        >
          <i :class="social.icon" class="text-xl"></i>
          <span class="text-xs font-bold tracking-widest uppercase">{{ social.name }}</span>
        </a>
      </div>

      <!-- Big Name -->
      <div class="text-center mb-10">
        <h2 class="text-6xl lg:text-9xl font-black tracking-tighter text-[var(--theme-text-strong)] opacity-5 uppercase leading-none select-none">
          VIJAY
        </h2>
      </div>

      <!-- Bottom Bar -->
      <div class="flex flex-col md:flex-row items-center justify-between gap-4 text-xs text-[var(--theme-text-muted)] font-['Oxanium'] tracking-wider uppercase">
        <span>Indore, India (GMT+5:30)</span>
        <span>Designing with Code</span>
        <span>&copy; {{ currentYear }} Vijay Diwaniya. All rights reserved.</span>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear();

const socials = [
  { name: 'GitHub', url: 'https://github.com/VIJAY33420', icon: 'bi bi-github' },
  { name: 'LinkedIn', url: 'https://linkedin.com/in/vijay-diwaniya-7b36aa3a4', icon: 'bi bi-linkedin' },
  { name: 'LeetCode', url: 'https://leetcode.com/u/VIJAY162004', icon: 'bi bi-code-slash' },
  { name: 'Twitter / X', url: 'https://x.com/VIJAY162004', icon: 'bi bi-twitter-x' },
  { name: 'YouTube', url: 'https://www.youtube.com/@VIJAYDIWANIYA-16', icon: 'bi bi-youtube' },
  { name: 'Sololearn', url: 'https://sololearn.com/en/profile/35629242', icon: 'bi bi-book' },
  { name: 'Email', url: 'mailto:vijay.diwaniya.cg@gmail.com', icon: 'bi bi-envelope-at' },
];
</script>

<style scoped>
.footer-social {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 12px 20px;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  color: var(--theme-text-muted);
  text-decoration: none;
  transition: all 0.3s ease;
}

.footer-social:hover {
  background: rgba(6, 182, 212, 0.1);
  border-color: rgba(6, 182, 212, 0.25);
  color: #22d3ee;
  transform: translateY(-3px);
  box-shadow: 0 8px 24px rgba(6, 182, 212, 0.15);
}

:global([data-theme="light"]) .footer-social {
  background: rgba(0, 0, 0, 0.03);
  border-color: rgba(0, 0, 0, 0.06);
}

:global([data-theme="light"]) .footer-social:hover {
  background: rgba(6, 182, 212, 0.08);
}
</style>
