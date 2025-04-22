<script setup>
import { ref, onMounted, computed } from "vue";
import img1 from "./assets/img1.jpg";
import img2 from "./assets/img2.jpg";
import img3 from "./assets/img3.jpg";
import img4 from "./assets/img4.jpg";
import img5 from "./assets/img5.jpg";
import img6 from "./assets/img6.jpg";
import img7 from "./assets/img7.jpg";
import img8 from "./assets/img8.jpg";
import img9 from "./assets/img9.jpg";
import img10 from "./assets/img10.jpg";
import img11 from "./assets/img11.jpg";
import img12 from "./assets/img12.jpg";

import Swiper from "swiper";
import { Navigation, Pagination, Autoplay } from "swiper/modules";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import gsap from "gsap";

const showAnimation = ref(false);
const startDate = new Date("2024-08-20"); // Substitua pela data real
const timeTogether = ref({
  years: 0,
  months: 0,
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

const totalDays = computed(() => {
  const now = new Date();
  const diff = now - startDate;
  return Math.floor(diff / (1000 * 60 * 60 * 24));
});

let swiper = null;

const photos = [
  {
    src: img1,
    caption: "O dia em que meu coração encontrou o seu 💘",
  },
  {
    src: img2,
    caption: "Aquele dia especial 💫",
  },
  {
    src: img3,
    caption: "Sempre juntos ✨",
  },
  {
    src: img4,
    caption: "Nosso amor em cada detalhe 💝",
  },
  {
    src: img5,
    caption: "Sorrisos que iluminam meu mundo 🌟",
  },
  {
    src: img6,
    caption: "Momentos que guardo no coração 💖",
  },
  {
    src: img7,
    caption: "Nossa história sendo escrita a cada dia 📖",
  },
  {
    src: img8,
    caption: "Olhares que dizem mais que palavras 👀",
  },
  {
    src: img9,
    caption: "Abraços que valem ouro 🤗",
  },
  {
    src: img10,
    caption: "Risadas que ecoam na memória 😄",
  },
  {
    src: img11,
    caption: "Amor que cresce a cada instante 🌱",
  },
  {
    src: img12,
    caption: "Você é meu porto seguro ⚓",
  },
];
const reasons = [
  "Seu sorriso é o meu raio de sol em dias nublados ☀️",
  "Sua força me inspira a ser melhor todos os dias 💪",
  "Você transforma meus dias com seu jeito único de ser ✨",
  "Seu carinho é o meu porto seguro em meio às tempestades 🌊",
  "Sua inteligência me encanta e me faz admirar você ainda mais 🧠",
  "Seu jeito de ser é perfeito, com todas as suas imperfeições 💫",
  "Você me entende como ninguém, até nos meus silêncios 🤫",
  "Seu amor é o combustível que me move todos os dias ⛽",
  "Sua companhia é o meu lugar favorito no mundo 🌎",
  "Você é a pessoa que eu escolhi para amar todos os dias da minha vida 💍",
];

const isPlaying = ref(true);

const toggleAudio = () => {
  isPlaying.value = !isPlaying.value;
  const iframe = document.querySelector("iframe");
  if (iframe) {
    if (isPlaying.value) {
      iframe.src = iframe.src.replace("autoplay=0", "autoplay=1");
    } else {
      iframe.src = iframe.src.replace("autoplay=1", "autoplay=0");
    }
  }
};

onMounted(() => {
  swiper = new Swiper(".swiper", {
    modules: [Navigation, Pagination, Autoplay],
    slidesPerView: 1,
    spaceBetween: 10,
    centeredSlides: true,
    loop: true,
    autoplay: {
      delay: 3000,
      disableOnInteraction: false,
    },
    pagination: {
      el: ".swiper-pagination",
      clickable: true,
      dynamicBullets: true,
    },
    navigation: {
      nextEl: ".swiper-button-next",
      prevEl: ".swiper-button-prev",
    },
    breakpoints: {
      320: {
        slidesPerView: 1,
        spaceBetween: 10,
      },
      480: {
        slidesPerView: 1,
        spaceBetween: 15,
      },
      640: {
        slidesPerView: 2,
        spaceBetween: 20,
      },
      1024: {
        slidesPerView: 3,
        spaceBetween: 30,
      },
    },
  });

  // Iniciar contador
  updateTimeTogether();
  setInterval(updateTimeTogether, 1000);

  // Adicionar efeitos de transição
  gsap.from(".section", {
    opacity: 0,
    y: 50,
    duration: 1,
    stagger: 0.3,
    ease: "power2.out",
    onComplete: () => {
      document.querySelectorAll(".section").forEach((section) => {
        section.style.opacity = "1";
        section.style.transform = "none";
      });
    },
  });
});

// Função para calcular o tempo juntos
const updateTimeTogether = () => {
  const now = new Date();
  const diff = now - startDate;

  timeTogether.value = {
    years: Math.floor(diff / (1000 * 60 * 60 * 24 * 365)),
    months: Math.floor(
      (diff % (1000 * 60 * 60 * 24 * 365)) / (1000 * 60 * 60 * 24 * 30)
    ),
    days: Math.floor(
      (diff % (1000 * 60 * 60 * 24 * 30)) / (1000 * 60 * 60 * 24)
    ),
    hours: Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
    minutes: Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60)),
    seconds: Math.floor((diff % (1000 * 60)) / 1000),
  };
};

const startForgivenessAnimation = () => {
  showAnimation.value = true;

  // Animação do botão
  gsap.to(".forgive-button", {
    scale: 1.2,
    duration: 0.3,
    yoyo: true,
    repeat: 1,
  });

  // Criar corações
  for (let i = 0; i < 50; i++) {
    const heart = document.createElement("div");
    heart.innerHTML = "❤️";
    heart.style.position = "fixed";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.top = "100vh";
    heart.style.fontSize = Math.random() * 20 + 10 + "px";
    heart.style.zIndex = "1000";
    document.body.appendChild(heart);

    gsap.to(heart, {
      y: -Math.random() * 500 - 100,
      x: Math.random() * 200 - 100,
      rotation: Math.random() * 360,
      duration: Math.random() * 2 + 2,
      ease: "power1.out",
      onComplete: () => heart.remove(),
    });
  }

  // Criar confetes
  for (let i = 0; i < 100; i++) {
    const confetti = document.createElement("div");
    confetti.style.position = "fixed";
    confetti.style.left = Math.random() * 100 + "vw";
    confetti.style.top = "0";
    confetti.style.width = "10px";
    confetti.style.height = "10px";
    confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
    confetti.style.borderRadius = "50%";
    confetti.style.zIndex = "1000";
    document.body.appendChild(confetti);

    gsap.to(confetti, {
      y: "100vh",
      x: Math.random() * 200 - 100,
      rotation: Math.random() * 360,
      duration: Math.random() * 2 + 2,
      ease: "power1.in",
      onComplete: () => confetti.remove(),
    });
  }

  // Animação da mensagem
  gsap.from(".animation-content", {
    scale: 0,
    rotation: 360,
    duration: 1,
    ease: "elastic.out(1, 0.5)",
  });

  // Efeito de pulso no coração
  gsap.to(".heart", {
    scale: 1.2,
    duration: 0.5,
    yoyo: true,
    repeat: -1,
    ease: "power1.inOut",
  });
};
</script>

<template>
  <div class="min-h-screen">
    <!-- Player de Áudio -->
    <div class="audio-player">
      <iframe
        width="0"
        height="0"
        src="https://www.youtube.com/embed/nzfU-jZ9te8?autoplay=1&loop=1&playlist=nzfU-jZ9te8"
        frameborder="0"
        allow="autoplay; encrypted-media"
        allowfullscreen
      ></iframe>
      <button class="audio-control" @click="toggleAudio">
        <span class="audio-icon">{{ isPlaying ? "🔊" : "🔈" }}</span>
        <span class="audio-text">{{
          isPlaying ? "Música Ligada" : "Música Desligada"
        }}</span>
      </button>
    </div>

    <!-- Header -->
    <header class="header">
      <h1 class="header-title">Desculpa, meu amor 💔</h1>
    </header>

    <!-- Contador de Tempo -->
    <section class="section time-counter">
      <h2 class="section-title">Nosso Tempo Juntos</h2>
      <div class="counter-container">
        <div class="counter-item">
          <span class="counter-number">{{ totalDays }}</span>
          <span class="counter-label">Dias de Amor</span>
        </div>
      </div>
      <div class="counter-subtitle">E contando... 💝</div>
    </section>

    <!-- Carta de Desculpas -->
    <section class="section">
      <div class="card">
        <p class="card-text">
          Oi, meu amor...<br /><br />
          Tô aqui com o coração apertado, escrevendo essas palavras porque sei
          que te magoei — e isso me dói demais. Você é a pessoa mais especial da
          minha vida, e só de imaginar que te deixei triste, meu peito
          aperta.<br /><br />
          Sei que nem sempre sou perfeito, mas meu amor por você é real, sincero
          e cheio de vontade de melhorar. Eu quero te fazer sorrir todos os
          dias, te dar segurança, carinho, e paz. Quero ser teu apoio, teu
          abraço, tua casa.<br /><br />
          A Bíblia diz que "o amor é paciente, o amor é bondoso" (1 Coríntios
          13:4), e é isso que quero viver com você. Também diz que "acima de
          tudo, amem-se sinceramente uns aos outros, porque o amor cobre uma
          multidão de pecados" (1 Pedro 4:8)... e eu confio que nosso amor é
          forte o bastante pra superar até isso.<br /><br />
          Você é a pessoa mais importante da minha vida, e quero te fazer feliz
          todos os dias. Prometo ser mais atento, mais carinhoso, mais presente.
          Você merece tudo de mais lindo, e eu quero ser quem te entrega isso,
          dia após dia.<br /><br />
          Te amo com todo o meu coração ❤️<br />
          <span class="signature-container">
            <span class="signature-text">Com amor,</span>
            <span class="signature-nickname">sua criaturinha</span>
          </span>
        </p>
      </div>
    </section>

    <!-- Galeria de Fotos -->
    <section class="gallery-section">
      <h2 class="section-title">Nossos Momentos Especiais</h2>
      <div class="swiper">
        <div class="swiper-wrapper">
          <div
            v-for="(photo, index) in photos"
            :key="index"
            class="swiper-slide"
          >
            <div class="photo-card">
              <img :src="photo.src" :alt="photo.caption" class="photo-image" />
              <div class="photo-caption">
                <p class="caption-text">{{ photo.caption }}</p>
              </div>
            </div>
          </div>
        </div>
        <div class="swiper-pagination"></div>
        <div class="swiper-button-prev"></div>
        <div class="swiper-button-next"></div>
      </div>
    </section>

    <!-- 10 Motivos -->
    <section class="section">
      <h2 class="section-title">10 motivos pelos quais te amo</h2>
      <ul class="reasons-list">
        <li v-for="(reason, index) in reasons" :key="index" class="reason-item">
          <span class="reason-number">{{ index + 1 }}.</span>
          <span class="reason-text">{{ reason }}</span>
        </li>
      </ul>
    </section>

    <!-- Botão de Perdão -->
    <section class="button-section">
      <button @click="startForgivenessAnimation" class="forgive-button">
        Clique aqui se me perdoa ❤️
      </button>
    </section>

    <!-- Animação de Perdão -->
    <div v-if="showAnimation" class="animation-modal">
      <div class="animation-content">
        <div class="heart">❤️</div>
        <p class="forgiveness-message">
          Você é incrível! Obrigado por me perdoar! 🎉
        </p>
        <p class="sub-message">
          Prometo ser melhor e te fazer feliz todos os dias! 💝
        </p>
      </div>
    </div>

    <!-- Rodapé -->
    <footer class="footer">
      <p class="footer-text">Estarei sempre aqui. Te amo! 💕</p>
    </footer>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;700&display=swap");

:root {
  --primary-50: #f5f3ff;
  --primary-100: #ede9fe;
  --primary-200: #ddd6fe;
  --primary-300: #c4b5fd;
  --primary-400: #a78bfa;
  --primary-500: #8b5cf6;
  --primary-600: #7c3aed;
  --primary-700: #6d28d9;
  --primary-800: #5b21b6;
  --primary-900: #4c1d95;
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  --radius-sm: 0.5rem;
  --radius-md: 1rem;
  --radius-lg: 1.5rem;
  --radius-xl: 2rem;
}

/* Reset e Base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}

body {
  margin: 0;
  min-height: 100vh;
  font-family: "Quicksand", sans-serif;
  background: linear-gradient(135deg, var(--primary-50), var(--primary-100));
  color: var(--primary-900);
  line-height: 1.6;
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}

/* Layout Principal */
.min-h-screen {
  min-height: 100vh;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  background: linear-gradient(
    135deg,
    rgba(245, 243, 255, 0.9),
    rgba(237, 233, 254, 0.9)
  );
  overflow-x: hidden;
}

/* Header */
.header {
  text-align: center;
  padding: 2rem 1rem;
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-md);
  backdrop-filter: blur(10px);
  border: 1px solid var(--primary-200);
  margin: 0 auto;
  width: 100%;
  max-width: 1200px;
}

.header-title {
  font-size: clamp(1.8rem, 5vw, 3rem);
  color: var(--primary-700);
  margin: 0;
  text-shadow: var(--shadow-sm);
  font-weight: 700;
  letter-spacing: -0.5px;
  line-height: 1.2;
}

/* Seções */
.section {
  max-width: 64rem;
  margin: 0 auto;
  padding: 1.5rem;
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-md);
  backdrop-filter: blur(10px);
  border: 1px solid var(--primary-200);
  width: 100%;
}

.section-title {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  color: var(--primary-700);
  text-align: center;
  margin-bottom: 2rem;
  font-weight: 600;
  letter-spacing: -0.5px;
  line-height: 1.2;
}

/* Card */
.card {
  background: white;
  padding: 1.5rem;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  color: var(--primary-900);
  line-height: 1.8;
  border: 1px solid var(--primary-200);
}

.card-text {
  font-size: clamp(1rem, 3vw, 1.2rem);
  line-height: 1.8;
  color: var(--primary-900);
  margin: 0;
}

/* Galeria */
.gallery-section {
  max-width: 80rem;
  margin: 0 auto;
  padding: 0.5rem;
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-md);
  backdrop-filter: blur(10px);
  width: 100%;
  overflow: hidden;
}

.swiper {
  width: 100%;
  padding: 0.5rem 0;
}

.swiper-slide {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 0.25rem;
}

.photo-card {
  position: relative;
  overflow: hidden;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-lg);
  aspect-ratio: 3/4;
  width: 100%;
  max-width: 300px;
  margin: 0 auto;
  transition: transform 0.3s ease;
  touch-action: manipulation;
}

.photo-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.photo-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  color: white;
  padding: 1rem;
  text-align: center;
}

.caption-text {
  margin: 0;
  font-size: 0.9rem;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  font-weight: 500;
}

/* Lista de Motivos */
.reasons-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 1.5rem;
}

.reason-item {
  background: white;
  padding: 1.5rem;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-sm);
  display: flex;
  align-items: center;
  font-size: 1.2rem;
  transition: all 0.3s ease;
  border: 1px solid var(--primary-100);
}

.reason-item:hover {
  transform: translateX(5px);
  box-shadow: var(--shadow-md);
  border-color: var(--primary-300);
}

.reason-number {
  color: var(--primary-600);
  font-weight: bold;
  margin-right: 1rem;
  min-width: 2.5rem;
  font-size: 1.4rem;
}

.reason-text {
  flex: 1;
  color: var(--primary-800);
}

/* Botão de Perdão */
.button-section {
  text-align: center;
  margin: 3rem 0;
}

.forgive-button {
  background: linear-gradient(45deg, var(--primary-500), var(--primary-700));
  color: white;
  padding: 1rem 2rem;
  border-radius: var(--radius-xl);
  border: none;
  font-size: clamp(1.1rem, 3vw, 1.4rem);
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: var(--shadow-lg);
  width: 90%;
  max-width: 500px;
  letter-spacing: 0.5px;
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
}

.forgive-button:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
  background: linear-gradient(45deg, var(--primary-600), var(--primary-800));
}

/* Animação de Perdão */
.animation-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.95);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  backdrop-filter: blur(5px);
}

.animation-content {
  text-align: center;
  padding: 3rem;
  background: white;
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-lg);
  width: 90%;
  max-width: 600px;
  border: 1px solid var(--primary-100);
}

.heart {
  font-size: 6rem;
  margin-bottom: 2rem;
  animation: pulse 1.5s infinite;
}

@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

.forgiveness-message {
  font-size: 2.5rem;
  color: var(--primary-700);
  margin-bottom: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.sub-message {
  font-size: 1.4rem;
  color: var(--primary-600);
  font-weight: 500;
}

/* Rodapé */
.footer {
  text-align: center;
  padding: 2rem;
  margin-top: auto;
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-md);
  backdrop-filter: blur(10px);
}

.footer-text {
  font-size: 1.2rem;
  color: var(--primary-700);
  font-weight: 500;
}

/* Contador de Tempo */
.time-counter {
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-xl);
  padding: 2rem;
  box-shadow: var(--shadow-md);
  backdrop-filter: blur(10px);
  text-align: center;
}

.counter-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 2rem 0;
}

.counter-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.counter-number {
  font-size: 4rem;
  font-weight: 700;
  color: var(--primary-700);
  line-height: 1;
  margin-bottom: 0.5rem;
  font-family: "Quicksand", sans-serif;
}

.counter-label {
  font-size: 1.2rem;
  color: var(--primary-600);
  text-transform: uppercase;
  letter-spacing: 2px;
}

.counter-subtitle {
  font-size: 1.1rem;
  color: var(--primary-600);
  font-style: italic;
  margin-top: 1rem;
  opacity: 0.8;
}

/* Estilos do Player de Áudio */
.audio-player {
  position: fixed;
  bottom: 1rem;
  right: 1rem;
  z-index: 1000;
}

.audio-control {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.25rem;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid var(--primary-200);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
}

.audio-control:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
  background: rgba(255, 255, 255, 1);
  border-color: var(--primary-300);
}

.audio-icon {
  font-size: 1.2rem;
}

.audio-text {
  font-size: 0.9rem;
  color: var(--primary-700);
  font-weight: 500;
}

/* Estilos da Assinatura */
.signature-container {
  display: block;
  margin-top: 1.5rem;
  text-align: right;
}

.signature-text {
  display: block;
  font-family: "Quicksand", sans-serif;
  font-size: 1.2rem;
  color: var(--primary-600);
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.signature-nickname {
  display: block;
  font-family: "Quicksand", cursive;
  font-size: 1.8rem;
  color: var(--primary-700);
  font-weight: 600;
  letter-spacing: 1px;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  transform: translateX(10px);
  transition: all 0.3s ease;
}

.signature-nickname:hover {
  transform: translateX(0);
  color: var(--primary-800);
}

/* Media Queries */
@media (max-width: 768px) {
  .min-h-screen {
    padding: 0.75rem;
    gap: 1.5rem;
  }

  .header {
    padding: 1.5rem 1rem;
  }

  .section {
    padding: 1.25rem;
  }

  .card {
    padding: 1.25rem;
  }

  .photo-card {
    max-width: 250px;
  }

  .forgive-button {
    padding: 0.75rem 1.5rem;
  }
}

@media (max-width: 480px) {
  .min-h-screen {
    padding: 0.5rem;
    gap: 1rem;
  }

  .header {
    padding: 1rem;
  }

  .section {
    padding: 1rem;
  }

  .card {
    padding: 1rem;
  }

  .photo-card {
    max-width: 200px;
  }

  .forgive-button {
    padding: 0.75rem 1rem;
  }

  .audio-control {
    padding: 0.5rem;
    border-radius: 50%;
  }

  .audio-text {
    display: none;
  }
}

@media (max-width: 320px) {
  .photo-card {
    max-width: 180px;
  }

  .forgive-button {
    padding: 0.5rem;
  }
}

/* Otimizações de Performance */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}

/* Suporte para Safari */
@supports (-webkit-touch-callout: none) {
  .min-h-screen {
    min-height: -webkit-fill-available;
  }
}
</style>
