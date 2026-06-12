<template>
  <NavBar />
  <router-view v-slot="{ Component }">
    <transition name="fade" mode="out-in">
      <component :is="Component" />
    </transition>
  </router-view>
  
  <footer class="footer">
    <p class="font-sans">© 2025 Gülbanu Yılmaz</p>
  </footer>
</template>

<script setup>
import NavBar from './components/NavBar.vue';
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.footer {
  text-align: center;
  padding: 2rem 0;
  border-top: 1px solid var(--border);
  margin-top: 4rem;
}

.footer p {
  font-size: 0.85rem;
  color: var(--text-muted);
  margin: 0;
}
</style>
