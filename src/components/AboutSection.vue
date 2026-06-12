<template>
  <section id="about" class="about-section container reveal" ref="sectionRef">
    <div class="about-content">
      <p class="about-text font-sans">
        Yazılım ve donanımın kesiştiği noktalarda çözümler üretmeyi seviyorum. 
        IoT sistemlerinden medikal görüntü işlemeye, mobil uygulamalardan yapay 
        zeka destekli arayüzlere kadar farklı alanlarda proje geliştirdim.
      </p>
      
      <div class="about-tags font-sans">
        <span class="outline-chip">Konya · Türkiye</span>
        <span class="outline-chip">Bilgisayar Mühendisliği</span>
        <span class="outline-chip">Açık İşbirliğine</span>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

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
.about-section {
  padding: 8rem 0;
  display: flex;
  justify-content: center;
}

.about-content {
  max-width: 800px;
  text-align: center;
}

.about-text {
  font-size: 1.5rem;
  line-height: 1.6;
  color: var(--text-primary);
  margin-bottom: 3rem;
  font-weight: 400;
}

.about-tags {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
}

@media (max-width: 768px) {
  .about-section {
    padding: 5rem 0;
  }
  
  .about-text {
    font-size: 1.25rem;
  }
}
</style>
