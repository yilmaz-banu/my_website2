<template>
  <section id="projects" class="py-20 w-full overflow-hidden bg-gray-50">
    <div class="container mx-auto px-4 text-center mb-12">
      <h2 class="text-4xl font-bold text-gray-800 mb-4">Öne Çıkan Çalışmalar</h2>
      <p class="text-gray-500">Seçili projeler — donanım, görüntü işleme ve mobil alanda</p>
    </div>

    <!-- Swiper Container -->
    <swiper
      :effect="'coverflow'"
      :grabCursor="true"
      :centeredSlides="true"
      slidesPerView="auto"
      :coverflowEffect="{
        rotate: 0,
        stretch: 0,
        depth: 200,
        modifier: 1,
        slideShadows: false,
      }"
      :autoplay="{
        delay: 3000,
        disableOnInteraction: false,
      }"
      :loop="true"
      :pagination="{ clickable: true }"
      :modules="modules"
      class="w-full py-10"
    >
      <!-- Proje Kartları (w ve h değerleri Tailwind ile sabitlendi) -->
      <swiper-slide
        v-for="(project, index) in exampleProjects"
        :key="index"
        class="custom-slide w-[320px] h-[450px]"
      >
        <div class="w-full h-full bg-white rounded-2xl shadow-2xl overflow-hidden flex flex-col border border-gray-100">
          <div class="p-8 flex-1 flex flex-col">
            <h3 class="text-2xl font-bold text-gray-800 mb-4">{{ project.title }}</h3>
            
            <p class="text-gray-600 leading-relaxed flex-1">
              {{ project.description }}
            </p>
            
            <div class="flex flex-wrap gap-2 mt-4">
              <span 
                v-for="(tag, tIndex) in project.tags" 
                :key="tIndex" 
                class="px-3 py-1 bg-gray-100 text-gray-600 text-xs font-semibold rounded-full uppercase tracking-wider"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </section>
</template>

<script setup>
// 1. Swiper Bileşenleri
import { Swiper, SwiperSlide } from 'swiper/vue';

// 2. KRİTİK: Swiper CSS Dosyaları
import 'swiper/css';
import 'swiper/css/effect-coverflow';
import 'swiper/css/pagination';

// 3. Swiper Modülleri
import { EffectCoverflow, Autoplay, Pagination } from 'swiper/modules';

// Modülleri Swiper'a tanıtmak için değişkene atama
const modules = [EffectCoverflow, Autoplay, Pagination];

// 4. Veri Yapısı (Örnek Projeler)
const exampleProjects = [
  {
    title: 'Akıllı Sera Sistemi',
    description: 'ESP32, kapasitif toprak nem sensörü ve Mamdani bulanık mantık kullanılarak iki farklı bitki odası için tasarlanmış otonom kontrol sistemi.',
    tags: ['C++', 'IoT', 'Fuzzy Logic']
  },
  {
    title: 'InnoPark AI Asistanı',
    description: 'Kurumsal bilgi kaynakları üzerinde çalışan, PHP ve NotebookLM destekli web tabanlı yapay zeka asistanı.',
    tags: ['PHP', 'AI', 'Web']
  },
  {
    title: 'Melanom Tespiti',
    description: 'Sayısal görüntü işleme teknikleri, morfolojik filtreleme ve DullRazor algoritması ile geliştirilen cilt lezyonu tespit projesi.',
    tags: ['MATLAB', 'Image Processing']
  }
];
</script>

<style scoped>
/* Swiper slide boyut davranışlarının bozulmasını engeller ve geçiş efekti verir */
.custom-slide {
  transition: opacity 0.4s ease-in-out;
}

/* Ekranın ortasında olmayan arka kartları %50 şeffaf yapar */
.swiper-slide:not(.swiper-slide-active) {
  opacity: 0.5;
}

/* Sayfalama (noktalar) tasarımı için ufak dokunuşlar */
:deep(.swiper-pagination-bullet) {
  background-color: #9ca3af; /* Tailwind gray-400 */
  opacity: 0.5;
}
:deep(.swiper-pagination-bullet-active) {
  background-color: #1f2937; /* Tailwind gray-800 */
  opacity: 1;
}
</style>