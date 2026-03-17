<script setup>
import { ref, computed } from "vue";
import srcQuiz from "../data/quiz.json";
import QuizCard from "../components/QuizCard.vue";

const quizes = ref(srcQuiz);
const search = ref("");

const filteredQuizes = computed(() => {
  return quizes.value.filter((quiz) =>
    quiz.title.toLowerCase().includes(search.value.toLowerCase()),
  );
});
</script>

<template>
  <div class="home-wrapper">
    <!-- Grid background -->
    <div class="grid-bg"></div>

    <!-- Floating orbs -->
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>

    <div class="home-inner">
      <!-- Header -->
      <header class="home-header">
        <div class="header-text">
          <span class="header-badge">
            <span class="badge-dot"></span>
            Selamat Datang
          </span>
          <h1 class="title">
            Uji <span class="title-gradient">Pengetahuan</span><br />Kamu Hari
            Ini
          </h1>
          <p class="subtitle">
            Pilih kategori quiz favorit dan tantang dirimu dengan soal-soal
            terbaik.
          </p>
        </div>

        <div class="search-wrapper">
          <svg
            class="search-icon"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <circle cx="11" cy="11" r="8" />
            <path d="m21 21-4.35-4.35" />
          </svg>
          <input
            type="text"
            class="search-input"
            v-model="search"
            placeholder="Cari quiz..."
          />
        </div>
      </header>

      <!-- Stats bar -->
      <div class="stats-bar">
        <div class="stat-item">
          <span class="stat-num">{{ quizes.length }}</span>
          <span class="stat-label">Total Quiz</span>
        </div>
        <div class="stat-divider"></div>
        <div class="stat-item">
          <span class="stat-num">{{ filteredQuizes.length }}</span>
          <span class="stat-label">Tersedia</span>
        </div>
        <div class="stat-divider"></div>
        <div class="stat-item">
          <span class="stat-num">∞</span>
          <span class="stat-label">Kesempatan</span>
        </div>
      </div>

      <!-- Empty state -->
      <div v-if="filteredQuizes.length === 0" class="empty-state">
        <div class="empty-icon">¯\_(ツ)_/¯</div>
        <p class="empty-title">Quiz tidak ditemukan</p>
        <p class="empty-sub">Coba kata kunci lain</p>
      </div>

      <!-- Grid -->
      <section class="quiz-grid">
        <QuizCard v-for="quiz in filteredQuizes" :key="quiz.id" :quiz="quiz" />
      </section>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Cabinet+Grotesk:wght@700;800;900&family=Satoshi:wght@400;500;700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@400;500;600;700&display=swap");

* {
  box-sizing: border-box;
}

.home-wrapper {
  min-height: 100vh;
  background: #0a0a0f;
  position: relative;
  overflow: hidden;
  font-family: "Outfit", sans-serif;
}

/* Grid background */
.grid-bg {
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 165, 0, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 165, 0, 0.03) 1px, transparent 1px);
  background-size: 60px 60px;
  pointer-events: none;
  z-index: 0;
}

/* Orbs */
.orb {
  position: fixed;
  border-radius: 50%;
  filter: blur(120px);
  pointer-events: none;
  z-index: 0;
}

.orb-1 {
  width: 600px;
  height: 600px;
  background: rgba(255, 140, 0, 0.12);
  top: -200px;
  right: -100px;
  animation: floatOrb 12s ease-in-out infinite;
}

.orb-2 {
  width: 400px;
  height: 400px;
  background: rgba(255, 60, 120, 0.08);
  bottom: 0;
  left: -100px;
  animation: floatOrb 16s ease-in-out infinite reverse;
}

.orb-3 {
  width: 300px;
  height: 300px;
  background: rgba(100, 200, 255, 0.06);
  top: 50%;
  left: 35%;
  animation: floatOrb 20s ease-in-out infinite;
}

@keyframes floatOrb {
  0%,
  100% {
    transform: translate(0, 0);
  }
  33% {
    transform: translate(30px, -30px);
  }
  66% {
    transform: translate(-20px, 20px);
  }
}

/* Inner */
.home-inner {
  position: relative;
  z-index: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 64px 40px;
}

/* Header */
.home-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: 40px;
  flex-wrap: wrap;
  gap: 32px;
}

.header-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #f97316;
  background: rgba(249, 115, 22, 0.1);
  border: 1px solid rgba(249, 115, 22, 0.25);
  border-radius: 100px;
  padding: 6px 14px;
  margin-bottom: 20px;
}

.badge-dot {
  width: 6px;
  height: 6px;
  background: #f97316;
  border-radius: 50%;
  animation: pulseDot 2s ease-in-out infinite;
}

@keyframes pulseDot {
  0%,
  100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.5;
    transform: scale(1.4);
  }
}

.title {
  font-family: "Bebas Neue", cursive;
  font-size: 72px;
  font-weight: 400;
  color: #ffffff;
  line-height: 0.95;
  margin: 0 0 16px;
  letter-spacing: 0.02em;
}

.title-gradient {
  background: linear-gradient(135deg, #f97316, #fb923c, #fbbf24);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  font-size: 15px;
  color: #64748b;
  margin: 0;
  max-width: 380px;
  line-height: 1.6;
}

/* Search */
.search-wrapper {
  position: relative;
  flex-shrink: 0;
}

.search-icon {
  position: absolute;
  left: 16px;
  top: 50%;
  transform: translateY(-50%);
  width: 16px;
  height: 16px;
  color: #475569;
  pointer-events: none;
}

.search-input {
  font-family: "Outfit", sans-serif;
  padding: 14px 20px 14px 44px;
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.08);
  background: rgba(255, 255, 255, 0.04);
  backdrop-filter: blur(12px);
  width: 280px;
  font-size: 14px;
  font-weight: 500;
  color: #e2e8f0;
  outline: none;
  transition: all 0.25s ease;
}

.search-input::placeholder {
  color: #334155;
}

.search-input:focus {
  border-color: rgba(249, 115, 22, 0.5);
  background: rgba(249, 115, 22, 0.05);
  box-shadow: 0 0 0 4px rgba(249, 115, 22, 0.1);
}

/* Stats */
.stats-bar {
  display: inline-flex;
  align-items: center;
  gap: 28px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 16px;
  padding: 16px 28px;
  margin-bottom: 48px;
  backdrop-filter: blur(10px);
}

.stat-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3px;
}

.stat-num {
  font-family: "Bebas Neue", cursive;
  font-size: 28px;
  color: #f97316;
  line-height: 1;
  letter-spacing: 0.05em;
}

.stat-label {
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #334155;
}

.stat-divider {
  width: 1px;
  height: 36px;
  background: rgba(255, 255, 255, 0.06);
}

/* Empty */
.empty-state {
  text-align: center;
  padding: 100px 20px;
}

.empty-icon {
  font-size: 32px;
  font-family: monospace;
  color: #334155;
  margin-bottom: 20px;
}

.empty-title {
  font-family: "Bebas Neue", cursive;
  font-size: 28px;
  color: #475569;
  margin: 0 0 8px;
  letter-spacing: 0.05em;
}

.empty-sub {
  font-size: 14px;
  color: #334155;
  margin: 0;
}

/* Grid */
.quiz-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
}
</style>
