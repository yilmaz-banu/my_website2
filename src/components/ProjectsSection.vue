<template>
  <section id="projects" class="py-24 container reveal" ref="sectionRef">
    <div class="text-center mb-16">
      <h2 class="text-4xl md:text-5xl font-serif text-text-primary mb-4">Öne Çıkan Çalışmalar</h2>
      <p class="text-text-muted font-sans text-base">Seçili projeler — donanım, görüntü işleme ve mobil alanda</p>
    </div>
    
    <div class="w-full">
      <swiper
        :effect="'coverflow'"
        :grabCursor="true"
        :centeredSlides="true"
        :slidesPerView="'auto'"
        :coverflowEffect="{
          rotate: 0,
          stretch: 0,
          depth: 250,
          modifier: 1,
          slideShadows: false,
        }"
        :autoplay="{
          delay: 3000,
          disableOnInteraction: false,
        }"
        :loop="true"
        :pagination="{
          clickable: true,
          dynamicBullets: true
        }"
        :modules="modules"
        class="projects-swiper"
      >
        <swiper-slide 
          v-for="project in projects" 
          :key="project.id" 
          class="swiper-slide-custom"
          @click="goToDetail(project.id)"
        >
          <div class="h-full flex flex-col bg-bg-card rounded-2xl border border-border overflow-hidden shadow-soft transition-transform duration-300 hover:border-accent-rose group cursor-pointer relative">
            <div class="absolute top-0 left-0 w-1 h-full bg-accent-rose opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
            
            <div class="p-8 flex-1 flex flex-col">
              <span class="text-4xl font-serif text-text-muted mb-4">{{ project.id }}</span>
              <h3 class="text-2xl font-bold font-sans text-text-primary mb-3">{{ project.title }}</h3>
              <p class="text-text-secondary font-sans leading-relaxed flex-1">{{ project.shortDesc }}</p>
              
              <div class="flex flex-wrap gap-2 mt-6">
                <span v-for="tag in project.tags.slice(0, 3)" :key="tag" class="text-xs font-mono text-text-muted uppercase tracking-wide px-3 py-1 border border-border rounded-full">{{ tag }}</span>
                <span v-if="project.tags.length > 3" class="text-xs font-mono text-text-muted uppercase tracking-wide px-3 py-1 border border-border rounded-full">+{{ project.tags.length - 3 }}</span>
              </div>
            </div>
            
            <div class="p-6 border-t border-border flex justify-end items-center bg-bg-secondary/30">
              <span class="text-text-primary text-2xl transition-transform duration-300 group-hover:translate-x-2">→</span>
            </div>
          </div>
        </swiper-slide>
      </swiper>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRouter } from 'vue-router';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/effect-coverflow';
import 'swiper/css/pagination';
import { EffectCoverflow, Pagination, Autoplay } from 'swiper/modules';
import { projects } from '../data/projects';

const modules = [EffectCoverflow, Pagination, Autoplay];
const router = useRouter();

const sectionRef = ref(null);
let observer = null;

const goToDetail = (id) => {
  router.push(`/projects/${id}`);
};

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
.projects-swiper {
  width: 100%;
  padding-top: 2rem;
  padding-bottom: 4rem; /* Pagination boşluğu */
}

.swiper-slide-custom {
  width: 300px;
  height: 420px;
  transition: filter 0.5s ease, opacity 0.5s ease;
}

@media (min-width: 768px) {
  .swiper-slide-custom {
    width: 380px;
    height: 480px;
  }
}

/* Yanlarda kalan projeleri hafif soluk ve bulanık yapma */
.swiper-slide:not(.swiper-slide-active) {
  opacity: 0.4;
  filter: blur(2px);
}

/* Özelleştirilmiş Pagination Noktaları */
:deep(.swiper-pagination-bullet) {
  background: var(--text-muted);
  opacity: 0.4;
  width: 10px;
  height: 10px;
  transition: all 0.3s ease;
}

:deep(.swiper-pagination-bullet-active) {
  background: var(--accent-rose);
  opacity: 1;
  width: 24px;
  border-radius: 5px;
}
</style>
