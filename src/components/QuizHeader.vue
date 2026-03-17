<script setup>
import { defineProps } from "vue";
const { questionPage, barPercentage } = defineProps([
  "questionPage",
  "barPercentage",
]);
</script>

<template>
  <header class="quiz-header">
    <div class="header-top">
      <div class="question-badge">
        <span class="badge-label">SOAL</span>
        <span class="badge-num">{{ questionPage }}</span>
      </div>
      <div class="progress-pill">
        <svg
          class="bolt-icon"
          viewBox="0 0 24 24"
          fill="currentColor"
          width="12"
          height="12"
        >
          <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z" />
        </svg>
        <span>{{ barPercentage }}</span>
      </div>
    </div>

    <div class="bar-track">
      <div class="bar-fill" :style="{ width: barPercentage }">
        <div class="bar-glow"></div>
      </div>
    </div>
  </header>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@400;500;600;700&display=swap");

.quiz-header {
  margin-bottom: 36px;
}

.header-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 14px;
}

.question-badge {
  display: flex;
  align-items: center;
  gap: 10px;
}

.badge-label {
  font-family: "Outfit", sans-serif;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: #334155;
}

.badge-num {
  font-family: "Bebas Neue", cursive;
  font-size: 22px;
  color: #e2e8f0;
  letter-spacing: 0.05em;
  line-height: 1;
}

.progress-pill {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: "Outfit", sans-serif;
  font-size: 12px;
  font-weight: 600;
  color: #f97316;
  background: rgba(249, 115, 22, 0.1);
  border: 1px solid rgba(249, 115, 22, 0.2);
  border-radius: 100px;
  padding: 5px 12px;
  letter-spacing: 0.04em;
}

.bolt-icon {
  color: #f97316;
}

/* Progress bar */
.bar-track {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.06);
  border-radius: 100px;
  overflow: visible;
  position: relative;
}

.bar-fill {
  height: 100%;
  background: linear-gradient(90deg, #f97316, #fbbf24);
  border-radius: 100px;
  transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

.bar-glow {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 16px;
  height: 16px;
  background: #f97316;
  border-radius: 50%;
  box-shadow: 0 0 12px 4px rgba(249, 115, 22, 0.6);
  animation: glowPulse 2s ease-in-out infinite;
}

@keyframes glowPulse {
  0%,
  100% {
    box-shadow: 0 0 12px 4px rgba(249, 115, 22, 0.6);
  }
  50% {
    box-shadow: 0 0 20px 8px rgba(249, 115, 22, 0.4);
  }
}
</style>
