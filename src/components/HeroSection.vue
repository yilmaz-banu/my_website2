<template>
  <section class="hero-section container">
    <!-- Sol kenar sabit ikonlar -->
    <div class="social-sidebar">
      <a href="https://github.com/yilmaz-banu" target="_blank" class="social-link">GH</a>
      <a href="https://www.linkedin.com/in/gülbanu-yılmaz-761514347/" target="_blank" class="social-link">IN</a>
    </div>

    <div class="hero-content">
      <div class="hero-left">
        <span class="subtitle font-sans">bilgisayar mühendisi adayı</span>
        <h1 class="title font-serif">
          <div class="name-line">
            <span v-for="(char, index) in 'Gülbanu'" :key="'g'+index" class="char" :style="{ animationDelay: `${index * 60}ms` }">{{ char }}</span>
          </div>
          <div class="name-line">
            <span v-for="(char, index) in 'Yılmaz'" :key="'y'+index" class="char" :style="{ animationDelay: `${(index + 7) * 60}ms` }">{{ char }}</span>
          </div>
        </h1>
        <p class="focus-areas font-sans">IoT · Görüntü İşleme · Mobil · Yapay Zeka</p>
        
        <div class="hero-actions font-sans">
          <a href="#" @click.prevent="scrollTo('projects')" class="btn btn-outline">Projeleri Gör</a>
          <a href="#" class="btn btn-ghost">CV İndir</a>
        </div>
      </div>
      
      <div class="hero-right">
        <!-- Tamamen CSS ile soyut geometrik şekil -->
        <div class="abstract-shape">
          <div class="circle"></div>
          <div class="line line-1"></div>
          <div class="line line-2"></div>
          <div class="line line-3"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const scrollTo = (id) => {
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: 'smooth' });
};
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding-top: 80px;
}

.social-sidebar {
  position: fixed;
  left: 2rem;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  z-index: 50;
}

.social-link {
  font-family: 'DM Mono', monospace;
  font-size: 0.8rem;
  color: var(--text-muted);
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  transition: color 0.3s ease;
}

.social-link:hover {
  color: var(--text-primary);
}

.hero-content {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
  padding-left: 4rem; /* social sidebar için yer */
}

.hero-left {
  flex: 1;
}

.subtitle {
  font-size: 0.9rem;
  color: var(--text-muted);
  text-transform: lowercase;
  letter-spacing: 0.5px;
  display: block;
  margin-bottom: 1rem;
}

.title {
  font-size: 96px;
  line-height: 1.1;
  letter-spacing: 2px;
  margin-bottom: 1.5rem;
}

.name-line {
  overflow: hidden;
}

.char {
  display: inline-block;
  opacity: 0;
  animation: fadeInChar 0.8s forwards;
}

@keyframes fadeInChar {
  to {
    opacity: 1;
  }
}

.focus-areas {
  font-size: 0.95rem;
  color: var(--text-muted);
  margin-bottom: 3rem;
}

.hero-actions {
  display: flex;
  gap: 1.5rem;
  align-items: center;
}

.btn {
  padding: 0.75rem 1.5rem;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  cursor: pointer;
}

.btn-outline {
  border: 1px solid var(--border);
  border-radius: 4px;
}

.btn-outline:hover {
  background-color: var(--bg-secondary);
}

.btn-ghost {
  position: relative;
  color: var(--text-secondary);
}

.btn-ghost::after {
  content: '';
  position: absolute;
  width: 100%;
  height: 1px;
  bottom: 0.5rem;
  left: 0;
  background-color: var(--text-primary);
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.3s ease;
}

.btn-ghost:hover {
  color: var(--text-primary);
}

.btn-ghost:hover::after {
  transform: scaleX(1);
  transform-origin: left;
}

.hero-right {
  flex: 1;
  display: flex;
  justify-content: flex-end;
  position: relative;
}

/* CSS Abstract Shape */
.abstract-shape {
  position: relative;
  width: 300px;
  height: 300px;
}

.circle {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 250px;
  height: 250px;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, var(--bg-card), var(--bg-secondary));
  box-shadow: 0 20px 40px var(--shadow);
}

.line {
  position: absolute;
  background-color: var(--accent-rose);
  opacity: 0.6;
}

.line-1 {
  width: 1px;
  height: 150px;
  top: 20px;
  left: 80px;
  transform: rotate(45deg);
}

.line-2 {
  width: 100px;
  height: 1px;
  bottom: 60px;
  right: 40px;
  background-color: var(--accent-sage);
}

.line-3 {
  width: 1px;
  height: 80px;
  top: 100px;
  right: 80px;
  transform: rotate(-15deg);
  background-color: var(--accent-lavender);
}

@media (max-width: 992px) {
  .title {
    font-size: 72px;
  }
  .hero-right {
    display: none;
  }
}

@media (max-width: 768px) {
  .title {
    font-size: 56px;
  }
  .hero-content {
    padding-left: 0;
  }
  .social-sidebar {
    display: none;
  }
}
</style>
