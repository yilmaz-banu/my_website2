<template>
  <nav :class="['navbar', { 'scrolled': isScrolled }]">
    <div class="container navbar-inner">
      <div class="logo font-serif" @click="goHome" style="cursor: pointer;">GY</div>
      <ul class="nav-links font-sans">
        <li><a href="#" @click.prevent="scrollTo('about')">Hakkımda</a></li>
        <li><a href="#" @click.prevent="scrollTo('experience')">Deneyim</a></li>
        <li><a href="#" @click.prevent="scrollTo('projects')">Projeler</a></li>
        <li><a href="#" @click.prevent="scrollTo('contact')">İletişim</a></li>
      </ul>
      <div class="lang-toggle font-sans">
        <span class="active">TR</span> / <span>EN</span>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRouter, useRoute } from 'vue-router';

const isScrolled = ref(false);
const router = useRouter();
const route = useRoute();

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20;
};

const goHome = () => {
  if (route.path !== '/') {
    router.push('/');
  } else {
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
};

const scrollTo = (id) => {
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const el = document.getElementById(id);
        if (el) el.scrollIntoView({ behavior: 'smooth' });
      }, 100);
    });
  } else {
    const el = document.getElementById(id);
    if (el) el.scrollIntoView({ behavior: 'smooth' });
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 100;
  padding: 1.5rem 0;
  transition: all 0.3s ease;
  border-bottom: 1px solid transparent;
}

.navbar.scrolled {
  padding: 1rem 0;
  background-color: rgba(250, 250, 248, 0.8);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
}

.navbar-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.5rem;
  font-weight: 600;
  letter-spacing: 1px;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-links a {
  font-size: 0.95rem;
  color: var(--text-secondary);
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: var(--text-primary);
}

.lang-toggle {
  font-size: 0.9rem;
  color: var(--text-muted);
  cursor: pointer;
}

.lang-toggle .active {
  color: var(--text-primary);
  font-weight: 500;
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
}
</style>
