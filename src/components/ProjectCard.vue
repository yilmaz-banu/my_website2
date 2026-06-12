<template>
  <div class="project-card" @click="goToDetail">
    <div class="card-left">
      <span class="project-num font-serif">{{ project.id }}</span>
    </div>
    
    <div class="card-middle">
      <h3 class="project-title font-sans">{{ project.title }}</h3>
      <p class="project-desc font-sans">{{ project.shortDesc }}</p>
      <div class="project-tags">
        <span v-for="tag in project.tags.slice(0, 3)" :key="tag" class="tag font-mono">{{ tag }}</span>
        <span v-if="project.tags.length > 3" class="tag font-mono">+{{ project.tags.length - 3 }}</span>
      </div>
    </div>
    
    <div class="card-right">
      <span class="arrow">→</span>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const props = defineProps({
  project: {
    type: Object,
    required: true
  }
});

const router = useRouter();

const goToDetail = () => {
  router.push(`/projects/${props.project.id}`);
};
</script>

<style scoped>
.project-card {
  display: flex;
  align-items: center;
  padding: 2rem 1.5rem;
  background-color: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.project-card::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 3px;
  background-color: var(--accent-rose);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 24px var(--shadow);
}

.project-card:hover::before {
  opacity: 1;
}

.project-card:hover .arrow {
  transform: translateX(4px);
}

.card-left {
  flex: 0 0 80px;
}

.project-num {
  font-size: 2rem;
  color: var(--text-muted);
}

.card-middle {
  flex: 1;
  padding-right: 2rem;
}

.project-title {
  font-size: 1.25rem;
  font-weight: 700;
  margin: 0 0 0.5rem 0;
}

.project-desc {
  font-size: 0.95rem;
  color: var(--text-secondary);
  margin: 0 0 1rem 0;
}

.project-tags {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.tag {
  font-size: 0.8rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.card-right {
  flex: 0 0 40px;
  display: flex;
  justify-content: flex-end;
}

.arrow {
  font-size: 1.5rem;
  color: var(--text-primary);
  transition: transform 0.3s ease;
}

@media (max-width: 768px) {
  .project-card {
    flex-direction: column;
    align-items: flex-start;
    padding: 1.5rem;
  }
  
  .card-left {
    flex: 0 0 auto;
    margin-bottom: 1rem;
  }
  
  .card-middle {
    padding-right: 0;
    margin-bottom: 1rem;
  }
  
  .card-right {
    align-self: flex-end;
  }
}
</style>
