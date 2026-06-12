<template>
  <div class="not-found container">
    <h1 class="title font-serif">404</h1>
    <p class="desc font-sans">Aradığınız sayfa bulunamadı.</p>
    <button class="back-btn font-sans" @click="$router.push('/')">Ana Sayfaya Dön</button>
  </div>
</template>

<style scoped>
.not-found {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-size: 6rem;
  margin-bottom: 1rem;
  color: var(--accent-rose);
}

.desc {
  font-size: 1.25rem;
  color: var(--text-secondary);
  margin-bottom: 2rem;
}

.back-btn {
  background: none;
  border: 1px solid var(--border);
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.back-btn:hover {
  background-color: var(--bg-secondary);
}
</style>
