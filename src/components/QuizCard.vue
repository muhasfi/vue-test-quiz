<script setup>
import { defineProps } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const { quiz } = defineProps(["quiz"]);

function goToQuiz() {
  router.push({ name: "quiz", params: { id: quiz.id } });
}
</script>

<template>
  <div class="card" @click="goToQuiz">
    <div class="card-img-wrapper">
      <img :src="quiz.img" :alt="quiz.title" />
      <div class="img-overlay"></div>
      <div class="question-badge">
        <svg viewBox="0 0 24 24" fill="currentColor" width="11" height="11">
          <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z" />
        </svg>
        {{ quiz.questions.length }} Soal
      </div>
    </div>

    <div class="card-body">
      <h2 class="card-title">{{ quiz.title }}</h2>
      <div class="card-footer">
        <span class="start-label">Mulai Quiz</span>
        <div class="arrow-btn">
          <svg
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2.5"
            width="14"
            height="14"
          >
            <path d="M5 12h14M12 5l7 7-7 7" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@400;500;600;700&display=swap");

.card {
  font-family: "Outfit", sans-serif;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.07);
  border-radius: 20px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
}

.card::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: 20px;
  background: linear-gradient(
    135deg,
    rgba(249, 115, 22, 0.06) 0%,
    transparent 60%
  );
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  z-index: 1;
}

.card:hover {
  border-color: rgba(249, 115, 22, 0.35);
  transform: translateY(-6px);
  box-shadow:
    0 0 0 1px rgba(249, 115, 22, 0.15),
    0 24px 48px rgba(0, 0, 0, 0.5);
}

.card:hover::before {
  opacity: 1;
}

/* Image */
.card-img-wrapper {
  position: relative;
  overflow: hidden;
}

.card-img-wrapper img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  display: block;
  transition: transform 0.4s ease;
  filter: brightness(0.8) saturate(0.9);
}

.card:hover .card-img-wrapper img {
  transform: scale(1.05);
  filter: brightness(0.7) saturate(0.8);
}

.img-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    transparent 40%,
    rgba(10, 10, 15, 0.8) 100%
  );
}

.question-badge {
  position: absolute;
  top: 12px;
  right: 12px;
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.06em;
  color: #f97316;
  background: rgba(10, 10, 15, 0.75);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(249, 115, 22, 0.3);
  border-radius: 100px;
  padding: 5px 11px;
}

/* Body */
.card-body {
  padding: 16px 20px 18px;
  position: relative;
  z-index: 2;
}

.card-title {
  font-family: "Outfit", sans-serif;
  font-size: 16px;
  font-weight: 700;
  color: #e2e8f0;
  margin: 0 0 16px;
  line-height: 1.4;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.start-label {
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #334155;
  transition: color 0.2s ease;
}

.card:hover .start-label {
  color: #f97316;
}

.arrow-btn {
  width: 32px;
  height: 32px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  display: flex;
  align-items: center;
  justify-content: center;
  color: #475569;
  transition: all 0.2s ease;
}

.card:hover .arrow-btn {
  background: linear-gradient(135deg, #f97316, #fbbf24);
  border-color: transparent;
  color: #0a0a0f;
  transform: translateX(3px);
}
</style>
