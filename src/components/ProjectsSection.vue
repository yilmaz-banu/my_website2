<template>
  <section id="projects" class="projects-section container reveal" ref="sectionRef">
    <div class="projects-header">
      <h2 class="section-title font-serif">Öne Çıkan Çalışmalar</h2>
      <p class="section-subtitle font-sans">Seçili projeler — donanım, görüntü işleme ve mobil alanda</p>
    </div>
    
    <div class="projects-list">
      <ProjectCard 
        v-for="project in projects" 
        :key="project.id" 
        :project="project" 
      />
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import ProjectCard from './ProjectCard.vue';
import { projects } from '../data/projects';

const sectionRef = ref(null);
let observer = null;

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('active');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });

  if (sectionRef.value) {
    observer.observe(sectionRef.value);
  }
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>

<style scoped>
.projects-section {
  padding: 6rem 0;
}

.projects-header {
  margin-bottom: 4rem;
  text-align: center;
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
}

.section-subtitle {
  font-size: 1rem;
  color: var(--text-muted);
}

.projects-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  max-width: 900px;
  margin: 0 auto;
}
</style>
