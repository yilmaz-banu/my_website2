<template>
  <section id="contact" class="contact-section container reveal" ref="sectionRef">
    <div class="contact-grid">
      <div class="contact-left">
        <h2 class="contact-title font-serif">Birlikte çalışalım</h2>
        <p class="contact-desc font-sans">Staj, proje veya iş birliği için ulaşabilirsiniz.</p>
        
        <div class="contact-links">
          <a href="https://github.com/yilmaz-banu" target="_blank" class="contact-link font-sans">
            <span class="icon">GH</span> GitHub
          </a>
          <a href="https://www.linkedin.com/in/gülbanu-yılmaz-761514347/" target="_blank" class="contact-link font-sans">
            <span class="icon">IN</span> LinkedIn
          </a>
        </div>
      </div>
      
      <div class="contact-right">
        <form @submit.prevent="sendEmail" class="contact-form">
          <div class="form-group">
            <label for="name" class="font-sans">Ad</label>
            <input type="text" id="name" v-model="form.name" required class="form-control font-sans" />
          </div>
          
          <div class="form-group">
            <label for="email" class="font-sans">E-posta</label>
            <input type="email" id="email" v-model="form.email" required class="form-control font-sans" />
          </div>
          
          <div class="form-group">
            <label for="message" class="font-sans">Mesaj</label>
            <textarea id="message" v-model="form.message" rows="4" required class="form-control font-sans"></textarea>
          </div>
          
          <button type="submit" class="btn-submit font-sans" :disabled="isSending">
            {{ isSending ? 'Gönderiliyor...' : 'Gönder' }}
          </button>
          
          <p v-if="successMessage" class="success-message font-sans">{{ successMessage }}</p>
          <p v-if="errorMessage" class="error-message font-sans">{{ errorMessage }}</p>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import emailjs from '@emailjs/browser';

const sectionRef = ref(null);
let observer = null;

const form = ref({
  name: '',
  email: '',
  message: ''
});

const isSending = ref(false);
const successMessage = ref('');
const errorMessage = ref('');

const sendEmail = () => {
  isSending.value = true;
  successMessage.value = '';
  errorMessage.value = '';

  const templateParams = {
    from_name: form.value.name,
    from_email: form.value.email,
    message: form.value.message,
  };

  // Placeholders from implementation plan
  emailjs.send(
    'YOUR_EMAILJS_SERVICE_ID',
    'YOUR_EMAILJS_TEMPLATE_ID',
    templateParams,
    'YOUR_EMAILJS_PUBLIC_KEY'
  ).then(
    (response) => {
      console.log('SUCCESS!', response.status, response.text);
      successMessage.value = 'Mesajınız başarıyla gönderildi.';
      form.value = { name: '', email: '', message: '' };
      isSending.value = false;
    },
    (error) => {
      console.log('FAILED...', error);
      errorMessage.value = 'Mesaj gönderilirken bir hata oluştu. Lütfen daha sonra tekrar deneyin.';
      isSending.value = false;
    }
  );
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
.contact-section {
  padding: 8rem 0;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  max-width: 1000px;
  margin: 0 auto;
}

.contact-title {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.contact-desc {
  font-size: 1.1rem;
  color: var(--text-secondary);
  margin-bottom: 3rem;
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-link {
  display: inline-flex;
  align-items: center;
  gap: 1rem;
  font-size: 1.1rem;
  color: var(--text-primary);
  transition: color 0.3s ease;
}

.contact-link:hover {
  color: var(--accent-rose);
}

.icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: var(--bg-secondary);
  font-family: 'DM Mono', monospace;
  font-size: 0.9rem;
  color: var(--text-secondary);
}

.contact-form {
  background-color: var(--bg-card);
  padding: 2.5rem;
  border-radius: 8px;
  border: 1px solid var(--border);
  box-shadow: 0 10px 30px var(--shadow);
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
  color: var(--text-secondary);
}

.form-control {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1px solid var(--border);
  border-radius: 4px;
  background-color: var(--bg-primary);
  color: var(--text-primary);
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  font-size: 1rem;
}

.form-control:focus {
  outline: none;
  border-color: var(--accent-sage);
  box-shadow: 0 0 0 3px rgba(157, 181, 160, 0.2);
}

textarea.form-control {
  resize: vertical;
}

.btn-submit {
  width: 100%;
  padding: 1rem;
  background-color: var(--text-primary);
  color: var(--bg-primary);
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-submit:hover:not(:disabled) {
  background-color: var(--text-secondary);
}

.btn-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.success-message {
  margin-top: 1rem;
  color: var(--accent-sage);
  font-size: 0.9rem;
}

.error-message {
  margin-top: 1rem;
  color: #e74c3c;
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
}
</style>
