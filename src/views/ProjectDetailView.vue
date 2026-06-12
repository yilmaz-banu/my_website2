<template>
  <div class="project-detail container" v-if="project">
    <button class="back-btn font-sans" @click="goBack">
      <span class="arrow">←</span> Geri
    </button>
    
    <header class="project-header">
      <h1 class="project-title font-serif">{{ project.title }}</h1>
      <hr class="divider" />
    </header>
    
    <div class="project-content">
      <p class="long-desc font-sans">{{ project.longDesc }}</p>
      
      <div class="tags font-sans">
        <span v-for="tag in project.tags" :key="tag" class="outline-chip">{{ tag }}</span>
      </div>
      
      <div class="project-links font-sans" v-if="project.github || project.demo">
        <a v-if="project.github" :href="project.github" target="_blank" class="btn btn-outline">GitHub'da Gör</a>
        <a v-if="project.demo" :href="project.demo" target="_blank" class="btn btn-outline">Canlı Demo</a>
      </div>
    </div>
    
    <section class="other-projects">
      <h3 class="other-title font-serif">Diğer Projeler</h3>
      <div class="other-list">
        <div 
          v-for="other in otherProjects" 
          :key="other.id" 
          class="other-card"
          @click="goToDetail(other.id)"
        >
          <h4 class="other-card-title font-sans">{{ other.title }}</h4>
          <span class="other-arrow">→</span>
        </div>
      </div>
    </section>
  </div>
  
  <div v-else class="not-found container">
    <h2 class="font-serif">Proje bulunamadı.</h2>
    <button class="back-btn font-sans" @click="goBack">Ana Sayfaya Dön</button>
  </div>
</template>

<script setup>
import { computed, onMounted, watch } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { projects } from '../data/projects';

const route = useRoute();
const router = useRouter();

const project = computed(() => {
  return projects.find(p => p.id === route.params.id);
});

const otherProjects = computed(() => {
  return projects.filter(p => p.id !== route.params.id).slice(0, 2);
});

const goBack = () => {
  router.push('/');
};

const goToDetail = (id) => {
  router.push(`/projects/${id}`);
};

onMounted(() => {
  window.scrollTo(0, 0);
});

watch(() => route.params.id, () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
});
</script>

<style scoped>
.project-detail {
  padding-top: 120px;
  padding-bottom: 6rem;
  max-width: 900px;
}

.back-btn {
  background: none;
  border: none;
  font-size: 1rem;
  color: var(--text-secondary);
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0;
  margin-bottom: 3rem;
  transition: color 0.3s ease;
}

.back-btn .arrow {
  transition: transform 0.3s ease;
}

.back-btn:hover {
  color: var(--text-primary);
}

.back-btn:hover .arrow {
  transform: translateX(-4px);
}

.project-title {
  font-size: 4rem;
  margin-bottom: 2rem;
  line-height: 1.1;
}

.divider {
  border: none;
  height: 1px;
  background-color: var(--border);
  margin-bottom: 3rem;
}

.long-desc {
  font-size: 1.15rem;
  line-height: 1.8;
  color: var(--text-primary);
  margin-bottom: 3rem;
}

.tags {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 3rem;
}

.project-links {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 6rem;
}

.btn {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  cursor: pointer;
  text-align: center;
}

.btn-outline {
  border: 1px solid var(--border);
  border-radius: 4px;
}

.btn-outline:hover {
  background-color: var(--bg-secondary);
}

.other-projects {
  border-top: 1px solid var(--border);
  padding-top: 4rem;
}

.other-title {
  font-size: 2rem;
  margin-bottom: 2rem;
}

.other-list {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.other-card {
  padding: 2rem;
  border: 1px solid var(--border);
  border-radius: 8px;
  background-color: var(--bg-card);
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.3s ease;
}

.other-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 20px var(--shadow);
  border-color: var(--accent-rose);
}

.other-card-title {
  font-size: 1.25rem;
  margin: 0;
}

.other-arrow {
  font-size: 1.25rem;
  transition: transform 0.3s ease;
}

.other-card:hover .other-arrow {
  transform: translateX(4px);
}

.not-found {
  padding-top: 150px;
  text-align: center;
}

.not-found h2 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
}

@media (max-width: 768px) {
  .project-title {
    font-size: 2.5rem;
  }
  
  .other-list {
    grid-template-columns: 1fr;
  }
}
</style>
