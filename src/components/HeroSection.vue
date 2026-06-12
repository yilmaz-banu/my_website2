<template>
  <section
    ref="heroRef"
    class="hero-section container overflow-hidden"
    :style="heroVars"
  >
    <div class="parallax-background" aria-hidden="true">
      <div class="data-wave data-wave-soft"></div>
      <div class="data-wave data-wave-fine"></div>

      <svg class="circuit-map" viewBox="0 0 1100 620" fill="none" role="presentation">
        <path
          class="circuit-line circuit-line-main"
          d="M36 436 C168 332 236 484 350 370 S568 210 706 296 S906 410 1062 236"
        />
        <path
          class="circuit-line circuit-line-soft"
          d="M74 184 C208 118 280 240 392 194 S606 70 738 168 S910 298 1036 142"
        />
        <path
          class="circuit-line circuit-line-soft"
          d="M138 536 C286 462 344 566 488 484 S674 356 818 424 S954 498 1058 374"
        />

        <g class="circuit-nodes">
          <circle cx="98" cy="386" r="4" />
          <circle cx="218" cy="376" r="5" />
          <circle cx="350" cy="370" r="4" />
          <circle cx="520" cy="258" r="6" />
          <circle cx="706" cy="296" r="5" />
          <circle cx="886" cy="394" r="4" />
          <circle cx="1006" cy="288" r="6" />
          <circle cx="170" cy="144" r="4" />
          <circle cx="392" cy="194" r="5" />
          <circle cx="612" cy="112" r="4" />
          <circle cx="818" cy="222" r="5" />
          <circle cx="264" cy="500" r="4" />
          <circle cx="488" cy="484" r="5" />
          <circle cx="676" cy="380" r="4" />
          <circle cx="932" cy="462" r="5" />
        </g>

        <g class="signal-ticks">
          <path d="M206 372 h28" />
          <path d="M506 256 h36" />
          <path d="M862 388 h32" />
          <path d="M378 190 h28" />
          <path d="M798 220 h32" />
          <path d="M470 480 h30" />
          <path d="M914 458 h36" />
        </g>
      </svg>

      <div class="micro-node node-a"></div>
      <div class="micro-node node-b"></div>
      <div class="micro-node node-c"></div>
      <div class="micro-node node-d"></div>
      <div class="micro-node node-e"></div>
    </div>

    <!-- Sol kenar sabit ikonlar -->
    <div class="social-sidebar">
      <a href="https://github.com/yilmaz-banu" target="_blank" rel="noreferrer" class="social-link">GH</a>
      <a href="https://www.linkedin.com/in/gülbanu-yılmaz-761514347/" target="_blank" rel="noreferrer" class="social-link">IN</a>
    </div>

    <div class="hero-content">
      <div class="hero-left">
        <span class="subtitle font-sans">bilgisayar mühendisi adayı</span>
        <h1 class="title font-serif">
          <div class="name-line">
            <span
              v-for="(char, index) in 'Gülbanu'"
              :key="'g' + index"
              class="char"
              :style="{ animationDelay: `${index * 60}ms` }"
            >
              {{ char }}
            </span>
          </div>
          <div class="name-line">
            <span
              v-for="(char, index) in 'Yılmaz'"
              :key="'y' + index"
              class="char"
              :style="{ animationDelay: `${(index + 7) * 60}ms` }"
            >
              {{ char }}
            </span>
          </div>
        </h1>
        <p class="focus-areas font-sans">IoT • Görüntü İşleme • Mobil • Yapay Zeka</p>

        <div class="hero-actions font-sans">
          <a href="#" @click.prevent="scrollTo('projects')" class="btn btn-outline">Projeleri Gör</a>
          <a href="#" class="btn btn-ghost">CV İndir</a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed, onMounted, onUnmounted, reactive, ref } from 'vue';

const heroRef = ref(null);

const motion = reactive({
  mouseX: 0,
  mouseY: 0,
  scrollY: 0,
});

const target = {
  mouseX: 0,
  mouseY: 0,
  scrollY: 0,
};

let rafId = 0;

const heroVars = computed(() => ({
  '--bg-x': `${motion.mouseX * -18}px`,
  '--bg-y': `${motion.mouseY * -12 + motion.scrollY * -0.18}px`,
  '--content-y': `${motion.scrollY * -0.08}px`,
}));

const scrollTo = (id) => {
  const el = document.getElementById(id);
  if (el) el.scrollIntoView({ behavior: 'smooth' });
};

const updateMouseTarget = (event) => {
  const rect = heroRef.value?.getBoundingClientRect();
  if (!rect) return;

  target.mouseX = (event.clientX - rect.left) / rect.width - 0.5;
  target.mouseY = (event.clientY - rect.top) / rect.height - 0.5;
};

const updateScrollTarget = () => {
  const rect = heroRef.value?.getBoundingClientRect();
  if (!rect) return;

  target.scrollY = Math.max(0, -rect.top);
};

const animate = () => {
  motion.mouseX += (target.mouseX - motion.mouseX) * 0.08;
  motion.mouseY += (target.mouseY - motion.mouseY) * 0.08;
  motion.scrollY += (target.scrollY - motion.scrollY) * 0.1;
  rafId = requestAnimationFrame(animate);
};

onMounted(() => {
  updateScrollTarget();
  window.addEventListener('mousemove', updateMouseTarget, { passive: true });
  window.addEventListener('scroll', updateScrollTarget, { passive: true });
  window.addEventListener('resize', updateScrollTarget, { passive: true });
  rafId = requestAnimationFrame(animate);
});

onUnmounted(() => {
  window.removeEventListener('mousemove', updateMouseTarget);
  window.removeEventListener('scroll', updateScrollTarget);
  window.removeEventListener('resize', updateScrollTarget);
  cancelAnimationFrame(rafId);
});
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding-top: 80px;
  isolation: isolate;
  background:
    radial-gradient(circle at 86% 24%, rgba(184, 176, 204, 0.11), transparent 28%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.48), rgba(250, 250, 248, 0));
}

.parallax-background {
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  transform: translate3d(var(--bg-x, 0), var(--bg-y, 0), 0);
  transition: transform 0.08s linear;
  opacity: 0.92;
}

.parallax-background::before {
  content: '';
  position: absolute;
  inset: 8% -8% 4% 12%;
  background-image:
    linear-gradient(rgba(160, 160, 160, 0.08) 1px, transparent 1px),
    linear-gradient(90deg, rgba(160, 160, 160, 0.08) 1px, transparent 1px);
  background-size: 72px 72px;
  mask-image: radial-gradient(circle at 62% 42%, black, transparent 70%);
}

.data-wave {
  position: absolute;
  right: -6%;
  width: 72%;
  border: 1px solid rgba(157, 181, 160, 0.16);
  border-color: rgba(157, 181, 160, 0.16) transparent transparent transparent;
  border-radius: 50%;
  animation: waveDrift 14s ease-in-out infinite alternate;
}

.data-wave-soft {
  top: 12%;
  height: 44%;
}

.data-wave-fine {
  top: 30%;
  height: 52%;
  width: 58%;
  border-color: rgba(201, 169, 154, 0.13) transparent transparent transparent;
  animation-duration: 18s;
  animation-delay: -5s;
}

.circuit-map {
  position: absolute;
  inset: 6% -4% auto auto;
  width: min(86vw, 1000px);
  height: auto;
  overflow: visible;
}

.circuit-line,
.signal-ticks path {
  stroke-linecap: round;
  stroke-linejoin: round;
  vector-effect: non-scaling-stroke;
}

.circuit-line-main {
  stroke: rgba(128, 144, 156, 0.27);
  stroke-width: 1.15;
  stroke-dasharray: 7 15;
  animation: dashFlow 18s linear infinite;
}

.circuit-line-soft {
  stroke: rgba(128, 144, 156, 0.16);
  stroke-width: 1;
  stroke-dasharray: 5 18;
  animation: dashFlow 24s linear infinite reverse;
}

.circuit-nodes circle {
  fill: rgba(255, 255, 255, 0.92);
  stroke: rgba(128, 144, 156, 0.28);
  stroke-width: 1;
  animation: nodePulse 5.6s ease-in-out infinite;
}

.circuit-nodes circle:nth-child(3n) {
  animation-delay: -1.6s;
}

.circuit-nodes circle:nth-child(4n) {
  animation-delay: -3s;
}

.signal-ticks path {
  stroke: rgba(184, 176, 204, 0.22);
  stroke-width: 1;
}

.micro-node {
  position: absolute;
  width: 7px;
  height: 7px;
  border: 1px solid rgba(128, 144, 156, 0.22);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.86);
  animation: floatNode 8s ease-in-out infinite;
}

.node-a {
  top: 18%;
  left: 48%;
}

.node-b {
  top: 34%;
  right: 18%;
  animation-delay: -2s;
}

.node-c {
  top: 66%;
  right: 9%;
  animation-delay: -4s;
}

.node-d {
  top: 72%;
  left: 56%;
  animation-delay: -5.5s;
}

.node-e {
  top: 44%;
  left: 72%;
  animation-delay: -1.2s;
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
  padding-left: 4rem;
  position: relative;
  z-index: 2;
  transform: translate3d(0, var(--content-y, 0), 0);
  will-change: transform;
}

.hero-left {
  flex: 1;
  max-width: 760px;
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
  position: relative;
  z-index: 3;
}

.btn-outline {
  border: 1px solid var(--border);
  border-radius: 4px;
  background: rgba(250, 250, 248, 0.62);
  backdrop-filter: blur(8px);
}

.btn-outline:hover {
  background-color: var(--bg-secondary);
}

.btn-ghost {
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

@keyframes fadeInChar {
  to {
    opacity: 1;
  }
}

@keyframes dashFlow {
  to {
    stroke-dashoffset: -220;
  }
}

@keyframes nodePulse {
  0%,
  100% {
    opacity: 0.58;
    transform: scale(1);
  }
  50% {
    opacity: 0.92;
    transform: scale(1.35);
  }
}

@keyframes floatNode {
  0%,
  100% {
    transform: translate3d(0, 0, 0);
    opacity: 0.5;
  }
  50% {
    transform: translate3d(10px, -14px, 0);
    opacity: 0.86;
  }
}

@keyframes waveDrift {
  from {
    transform: translate3d(-10px, 4px, 0) rotate(-2deg);
  }
  to {
    transform: translate3d(16px, -10px, 0) rotate(2deg);
  }
}

@media (prefers-reduced-motion: reduce) {
  .parallax-background,
  .hero-content,
  .data-wave,
  .circuit-line-main,
  .circuit-line-soft,
  .circuit-nodes circle,
  .micro-node,
  .char {
    animation: none;
    transition: none;
    transform: none;
  }

  .char {
    opacity: 1;
  }
}

@media (max-width: 992px) {
  .title {
    font-size: 72px;
  }

  .circuit-map {
    right: -38%;
    width: 118vw;
    opacity: 0.7;
  }
}

@media (max-width: 768px) {
  .hero-section {
    min-height: 92vh;
  }

  .title {
    font-size: 56px;
  }

  .hero-content {
    padding-left: 0;
  }

  .social-sidebar {
    display: none;
  }

  .parallax-background::before {
    inset: 18% -34% 10% 8%;
    background-size: 58px 58px;
  }

  .circuit-map {
    inset: 14% auto auto 16%;
    width: 140vw;
  }
}
</style>
