<template>
  <div id="contact" class="contact-wrapper">
    <section class="contact-section relative min-h-screen overflow-hidden">
      <div class="contact-bg absolute inset-0 z-0" aria-hidden="true">
        <div class="absolute inset-0 bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900"></div>
        <div class="absolute top-0 right-0 w-[600px] h-[600px] bg-cyan-500/5 rounded-full blur-[150px]"></div>
        <div class="absolute bottom-0 left-0 w-[500px] h-[500px] bg-[rgba(224,172,105,0.05)] rounded-full blur-[120px]"></div>
      </div>

      <div class="contact-split relative z-20">
        <div class="contact-left">
          <div class="contact-left-content">
            <span class="inline-block px-6 py-2 rounded-full bg-cyan-500/10 border border-cyan-500/20 text-cyan-400 text-xs font-black tracking-widest uppercase mb-6">
              Get In Touch
            </span>
            <h2 class="text-4xl lg:text-6xl font-black tracking-tight text-white leading-tight mb-6">
              Let's Build<br>
              <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">Something Great</span>
            </h2>
            <p class="text-lg text-gray-400 leading-relaxed max-w-md font-['Oxanium']">
              Have a project idea or opportunity? I'm always open to discussing new challenges and collaborations.
            </p>

            <!-- Social Links Bar -->
            <div class="mt-10 flex flex-wrap gap-3">
              <a v-for="social in socials" :key="social.name" :href="social.url" target="_blank" rel="noopener noreferrer"
                class="social-pill group" :title="social.name">
                <i :class="social.icon" class="text-lg"></i>
                <span class="social-pill-label">{{ social.name }}</span>
              </a>
            </div>
          </div>
        </div>

        <div class="contact-right" :class="{ 'is-success': formSubmitted }">
          <!-- Success State -->
          <div v-if="formSubmitted" class="contact-success-wrapper">
            <div class="w-20 h-20 rounded-full bg-green-500/20 border border-green-500/30 flex items-center justify-center mb-6">
              <svg xmlns="http://www.w3.org/2000/svg" class="w-10 h-10 text-green-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <polyline points="20 6 9 17 4 12"></polyline>
              </svg>
            </div>
            <h3 class="text-2xl font-black text-white mb-3">Message Sent!</h3>
            <p class="text-gray-400 text-center max-w-sm font-['Oxanium']">
              Thanks for reaching out. I'll get back to you soon!
            </p>
          </div>

          <!-- Form State -->
          <div v-else class="contact-form-wrapper">
            <h3 class="text-xl font-black text-white mb-8 tracking-tight">Send me a message</h3>

            <!-- Toast notification -->
            <div
              v-if="toastMessage"
              class="fixed top-6 right-6 z-[300] px-6 py-3 rounded-xl text-sm font-bold shadow-xl"
              :class="toastType === 'success'
                ? 'bg-green-500/90 text-white border border-green-400/30'
                : 'bg-red-500/90 text-white border border-red-400/30'"
            >
              {{ toastMessage }}
            </div>

            <form
              :action="formspreeUrl"
              method="POST"
              class="space-y-6"
              @submit.prevent="handleSubmit"
              novalidate
            >
              <div>
                <label class="block text-xs font-bold text-gray-400 uppercase tracking-widest mb-2">Name</label>
                <input
                  v-model.trim="form.name"
                  type="text"
                  name="name"
                  placeholder="Your name"
                  class="contact-input"
                  :class="{ 'border-red-500/50': errors.name }"
                  @blur="validateField('name')"
                />
                <p v-if="errors.name" class="mt-1 text-xs text-red-400">{{ errors.name }}</p>
              </div>

              <div>
                <label class="block text-xs font-bold text-gray-400 uppercase tracking-widest mb-2">Email</label>
                <input
                  v-model.trim="form.email"
                  type="email"
                  name="email"
                  placeholder="your@email.com"
                  class="contact-input"
                  :class="{ 'border-red-500/50': errors.email }"
                  @blur="validateField('email')"
                />
                <p v-if="errors.email" class="mt-1 text-xs text-red-400">{{ errors.email }}</p>
              </div>

              <div>
                <label class="block text-xs font-bold text-gray-400 uppercase tracking-widest mb-2">Message</label>
                <textarea
                  v-model.trim="form.message"
                  name="message"
                  rows="5"
                  placeholder="Tell me about your project or idea..."
                  class="contact-input resize-none"
                  :class="{ 'border-red-500/50': errors.message }"
                  @blur="validateField('message')"
                ></textarea>
                <p v-if="errors.message" class="mt-1 text-xs text-red-400">{{ errors.message }}</p>
              </div>

              <button
                type="submit"
                :disabled="isSubmitting"
                class="w-full py-4 rounded-xl font-black text-sm uppercase tracking-widest bg-gradient-to-r from-cyan-500 to-blue-600 text-white transition-all duration-300 hover:shadow-lg hover:shadow-cyan-500/25 hover:-translate-y-0.5 disabled:opacity-50 disabled:cursor-not-allowed"
              >
                {{ isSubmitting ? 'Sending...' : 'Send Message' }}
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const formspreeUrl = 'https://formspree.io/f/mvzdardl';

const form = ref({ name: '', email: '', message: '' });
const errors = ref({ name: '', email: '', message: '' });
const isSubmitting = ref(false);
const formSubmitted = ref(false);
const toastMessage = ref('');
const toastType = ref('success');

const socials = [
  { name: 'GitHub', url: 'https://github.com/VIJAY33420', icon: 'bi bi-github' },
  { name: 'LinkedIn', url: 'https://linkedin.com/in/vijay-diwaniya-7b36aa3a4', icon: 'bi bi-linkedin' },
  { name: 'LeetCode', url: 'https://leetcode.com/u/VIJAY162004', icon: 'bi bi-code-slash' },
  { name: 'Twitter', url: 'https://x.com/VIJAY162004', icon: 'bi bi-twitter-x' },
  { name: 'YouTube', url: '#', icon: 'bi bi-youtube' }, // TODO: Add your YouTube channel URL
  { name: 'Sololearn', url: 'https://sololearn.com/en/profile/35629242', icon: 'bi bi-book' },
];

const showToast = (message, type = 'success') => {
  toastMessage.value = message;
  toastType.value = type;
  setTimeout(() => { toastMessage.value = ''; }, 4000);
};

const validateField = (field) => {
  if (field === 'name' && !form.value.name) {
    errors.value.name = 'Please enter your name';
    return false;
  }
  if (field === 'email') {
    if (!form.value.email) {
      errors.value.email = 'Please enter your email';
      return false;
    }
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(form.value.email)) {
      errors.value.email = 'Please enter a valid email';
      return false;
    }
  }
  if (field === 'message' && !form.value.message) {
    errors.value.message = 'Please enter a message';
    return false;
  }
  errors.value[field] = '';
  return true;
};

const handleSubmit = async () => {
  const nameValid = validateField('name');
  const emailValid = validateField('email');
  const messageValid = validateField('message');
  if (!nameValid || !emailValid || !messageValid) return;

  isSubmitting.value = true;

  try {
    const response = await fetch(formspreeUrl, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'Accept': 'application/json' },
      body: JSON.stringify({
        name: form.value.name,
        email: form.value.email,
        message: form.value.message
      })
    });

    if (response.ok) {
      formSubmitted.value = true;
      showToast('Message sent successfully!', 'success');
      form.value = { name: '', email: '', message: '' };
    } else {
      throw new Error('Failed');
    }
  } catch {
    showToast('Failed to send message. Please try again.', 'error');
  } finally {
    isSubmitting.value = false;
  }
};
</script>

<style scoped>
.contact-wrapper {
  position: relative;
}

.contact-section {
  position: relative;
  background: linear-gradient(135deg, #0a0f19, #111827);
}

.contact-split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 100vh;
}

.contact-left {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3rem;
}

.contact-left-content {
  max-width: 520px;
}

.contact-right {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3rem;
  background: rgba(255, 255, 255, 0.02);
  border-left: 1px solid rgba(255, 255, 255, 0.06);
}

.contact-form-wrapper,
.contact-success-wrapper {
  width: 100%;
  max-width: 460px;
}

.contact-success-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.contact-input {
  width: 100%;
  padding: 14px 18px;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: white;
  font-size: 15px;
  font-family: 'Oxanium', sans-serif;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  outline: none;
}

.contact-input::placeholder {
  color: rgba(255, 255, 255, 0.25);
}

.contact-input:focus {
  border-color: rgba(6, 182, 212, 0.5);
  box-shadow: 0 0 0 3px rgba(6, 182, 212, 0.1);
}

.social-pill {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 16px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: var(--theme-text-muted, #9ca3af);
  font-size: 13px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.25s ease;
}

.social-pill:hover {
  background: rgba(6, 182, 212, 0.15);
  border-color: rgba(6, 182, 212, 0.3);
  color: #22d3ee;
  transform: translateY(-2px);
}

.social-pill-label {
  font-size: 11px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

@media (max-width: 768px) {
  .contact-split {
    grid-template-columns: 1fr;
  }

  .contact-left {
    padding: 2rem 1.5rem;
    text-align: center;
  }

  .contact-left-content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .contact-right {
    border-left: none;
    border-top: 1px solid rgba(255, 255, 255, 0.06);
    padding: 2rem 1.5rem;
  }
}

:global([data-theme="light"]) .contact-section {
  background: linear-gradient(135deg, #f8fafc, #e2e8f0);
}

:global([data-theme="light"]) .contact-input {
  background: white;
  border-color: rgba(0, 0, 0, 0.1);
  color: #1e293b;
}

:global([data-theme="light"]) .contact-input::placeholder {
  color: rgba(0, 0, 0, 0.3);
}

:global([data-theme="light"]) .contact-right {
  background: rgba(0, 0, 0, 0.02);
  border-left-color: rgba(0, 0, 0, 0.06);
}

:global([data-theme="light"]) .social-pill {
  background: rgba(0, 0, 0, 0.04);
  border-color: rgba(0, 0, 0, 0.08);
  color: #64748b;
}
</style>
