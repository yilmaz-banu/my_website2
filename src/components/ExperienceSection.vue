<template>
  <section id="experience" class="experience-section container reveal" ref="sectionRef">
    <div class="experience-content">
      <h2 class="section-title font-serif">Deneyim</h2>
      
      <div class="timeline-container">
        <div class="timeline-line" ref="lineRef"></div>
        
        <div class="timeline-items">
          <div v-for="(exp, index) in experiences" :key="index" class="timeline-item reveal" :ref="el => { if(el) itemsRef[index] = el }">
            <div class="timeline-dot"></div>
            <div class="timeline-content">
              <div class="timeline-header">
                <h3 class="role font-sans">{{ exp.role }}</h3>
                <span class="year font-mono">{{ exp.year }}</span>
              </div>
              <p class="company font-serif">{{ exp.company }}</p>
              <p class="description font-sans">{{ exp.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const experiences = [
  {
    company: 'InnoPark · Konya',
    role: 'Stajyer Web Geliştirici',
    year: '2023',
    description: 'Yemekhane yönetim sistemi için web tabanlı arayüz, veritabanı bağlantısı ve işlevsel akışlar.'
  },
  {
    company: 'Dpointgroup · Barcelona',
    role: 'Stajyer Yazılım Geliştirici',
    year: '2024',
    description: 'Stajyer yönetim süreçlerini dijitalleştiren mobil uygulama. Arayüz akışları ve veri yönetimi odaklı.'
  },
  {
    company: 'Gönüllü',
    role: 'Robotik Kodlama Eğitmenliği',
    year: '2024',
    description: 'Ortaokul öğrencilerine proje tabanlı robotik kodlama eğitimi.'
  },
  {
    company: 'InnoPark · Konya',
    role: 'Stajyer Yazılım Geliştirici',
    year: '2025',
    description: 'Vue.js ile arayüz geliştirme, bileşen mimarisi ve kurumsal web uygulaması geliştirme.'
  }
];

const sectionRef = ref(null);
const lineRef = ref(null);
const itemsRef = ref([]);
let observer = null;

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        if (entry.target === sectionRef.value) {
          entry.target.classList.add('active');
          if (lineRef.value) {
            lineRef.value.style.height = '100%';
          }
        } else {
          entry.target.classList.add('active');
        }
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });

  if (sectionRef.value) {
    observer.observe(sectionRef.value);
  }
  
  itemsRef.value.forEach(item => {
    if (item) observer.observe(item);
  });
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>

<style scoped>
.experience-section {
  padding: 6rem 0;
}

.experience-content {
  max-width: 800px;
  margin: 0 auto;
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 4rem;
  text-align: center;
}

.timeline-container {
  position: relative;
  padding-left: 2rem;
}

.timeline-line {
  position: absolute;
  left: 0;
  top: 0;
  width: 1px;
  height: 0;
  background-color: var(--border);
  transition: height 1.5s cubic-bezier(0.25, 0.1, 0.25, 1);
}

.timeline-items {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.timeline-item {
  position: relative;
}

.timeline-dot {
  position: absolute;
  left: -2.35rem;
  top: 0.4rem;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background-color: var(--bg-primary);
  border: 1px solid var(--accent-rose);
  z-index: 2;
}

.timeline-content {
  background-color: var(--bg-card);
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 20px var(--shadow);
  border: 1px solid var(--border);
}

.timeline-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.role {
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0;
}

.year {
  font-size: 0.9rem;
  color: var(--text-muted);
}

.company {
  font-size: 1.2rem;
  color: var(--accent-rose);
  margin: 0 0 1rem 0;
}

.description {
  font-size: 0.95rem;
  color: var(--text-secondary);
  line-height: 1.6;
  margin: 0;
}

@media (max-width: 768px) {
  .timeline-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
  }
  
  .timeline-content {
    padding: 1.5rem;
  }
}
</style>
