<script setup>
import { computed } from "vue";

const { quizQuestionsLength, numberOfCorrectAnswer } = defineProps([
  "quizQuestionsLength",
  "numberOfCorrectAnswer",
]);

const percentage = computed(() =>
  Math.round((numberOfCorrectAnswer / quizQuestionsLength) * 100),
);

const grade = computed(() => {
  if (percentage.value >= 80)
    return {
      label: "Luar Biasa!",
      emoji: "🏆",
      color: "#f97316",
      glow: "rgba(249,115,22,0.3)",
    };
  if (percentage.value >= 60)
    return {
      label: "Bagus!",
      emoji: "👍",
      color: "#22d3ee",
      glow: "rgba(34,211,238,0.3)",
    };
  if (percentage.value >= 40)
    return {
      label: "Lumayan!",
      emoji: "💪",
      color: "#fbbf24",
      glow: "rgba(251,191,36,0.3)",
    };
  return {
    label: "Ayo Coba Lagi!",
    emoji: "🔄",
    color: "#ef4444",
    glow: "rgba(239,68,68,0.3)",
  };
});
</script>

<template>
  <section class="results">
    <!-- Top badge -->
    <div
      class="grade-badge"
      :style="{
        color: grade.color,
        borderColor: grade.color + '33',
        background: grade.color + '11',
      }"
    >
      <span>{{ grade.emoji }}</span>
      <span class="grade-label">{{ grade.label }}</span>
    </div>

    <!-- Score ring -->
    <div class="score-ring-wrapper">
      <div class="ring-outer" :style="{ boxShadow: `0 0 60px ${grade.glow}` }">
        <svg viewBox="0 0 140 140" class="ring-svg">
          <circle cx="70" cy="70" r="58" class="ring-bg" />
          <circle
            cx="70"
            cy="70"
            r="58"
            class="ring-fill"
            :style="{
              strokeDasharray: `${(364 * percentage) / 100} 364`,
              stroke: grade.color,
            }"
          />
        </svg>
        <div class="score-center">
          <span class="score-num" :style="{ color: grade.color }">{{
            numberOfCorrectAnswer
          }}</span>
          <span class="score-sep">/{{ quizQuestionsLength }}</span>
        </div>
      </div>
    </div>

    <!-- Percentage -->
    <div class="pct-display">
      <span class="pct-num" :style="{ color: grade.color }">{{
        percentage
      }}</span>
      <span class="pct-symbol">%</span>
    </div>
    <p class="pct-label">jawaban benar</p>

    <!-- Stats row -->
    <div class="stats-row">
      <div class="stat-box correct">
        <span class="stat-val">{{ numberOfCorrectAnswer }}</span>
        <span class="stat-name">Benar</span>
      </div>
      <div class="stat-sep"></div>
      <div class="stat-box wrong">
        <span class="stat-val">{{
          quizQuestionsLength - numberOfCorrectAnswer
        }}</span>
        <span class="stat-name">Salah</span>
      </div>
      <div class="stat-sep"></div>
      <div class="stat-box total">
        <span class="stat-val">{{ quizQuestionsLength }}</span>
        <span class="stat-name">Total</span>
      </div>
    </div>

    <RouterLink to="/" class="back-btn">
      <svg
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2.5"
        width="15"
        height="15"
      >
        <path d="M3 9l9-7 9 7v11a2 2 0 01-2 2H5a2 2 0 01-2-2z" />
        <polyline points="9 22 9 12 15 12 15 22" />
      </svg>
      Kembali ke Home
    </RouterLink>
  </section>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@400;500;600;700&display=swap");

.results {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 16px 0 8px;
  font-family: "Outfit", sans-serif;
}

.grade-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.06em;
  border: 1px solid;
  border-radius: 100px;
  padding: 8px 18px;
  margin-bottom: 32px;
}

.grade-label {
  text-transform: uppercase;
}

/* Ring */
.score-ring-wrapper {
  margin-bottom: 24px;
}

.ring-outer {
  border-radius: 50%;
  padding: 4px;
  position: relative;
}

.ring-svg {
  width: 160px;
  height: 160px;
  transform: rotate(-90deg);
  display: block;
}

.ring-bg {
  fill: none;
  stroke: rgba(255, 255, 255, 0.06);
  stroke-width: 10;
}

.ring-fill {
  fill: none;
  stroke-width: 10;
  stroke-linecap: round;
  transition: stroke-dasharray 1.2s cubic-bezier(0.4, 0, 0.2, 1);
}

.score-center {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.score-num {
  font-family: "Bebas Neue", cursive;
  font-size: 52px;
  line-height: 1;
  letter-spacing: 0.02em;
}

.score-sep {
  font-family: "Outfit", sans-serif;
  font-size: 14px;
  font-weight: 500;
  color: #334155;
  margin-top: 2px;
}

/* Percentage display */
.pct-display {
  display: flex;
  align-items: baseline;
  gap: 4px;
  margin-bottom: 6px;
}

.pct-num {
  font-family: "Bebas Neue", cursive;
  font-size: 64px;
  line-height: 1;
  letter-spacing: 0.02em;
}

.pct-symbol {
  font-family: "Bebas Neue", cursive;
  font-size: 32px;
  color: #475569;
}

.pct-label {
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #334155;
  margin: 0 0 32px;
}

/* Stats row */
.stats-row {
  display: flex;
  align-items: center;
  gap: 24px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.07);
  border-radius: 16px;
  padding: 16px 32px;
  margin-bottom: 36px;
  width: 100%;
  max-width: 320px;
  justify-content: center;
}

.stat-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
}

.stat-val {
  font-family: "Bebas Neue", cursive;
  font-size: 28px;
  line-height: 1;
  letter-spacing: 0.05em;
}

.stat-name {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #334155;
}

.correct .stat-val {
  color: #4ade80;
}
.wrong .stat-val {
  color: #f87171;
}
.total .stat-val {
  color: #94a3b8;
}

.stat-sep {
  width: 1px;
  height: 40px;
  background: rgba(255, 255, 255, 0.06);
}

/* Back button */
.back-btn {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 14px 28px;
  background: linear-gradient(135deg, #f97316, #fbbf24);
  color: #0a0a0f;
  font-family: "Outfit", sans-serif;
  font-size: 14px;
  font-weight: 700;
  border-radius: 14px;
  text-decoration: none;
  letter-spacing: 0.04em;
  box-shadow: 0 4px 20px rgba(249, 115, 22, 0.4);
  transition: all 0.2s ease;
}

.back-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 32px rgba(249, 115, 22, 0.55);
}
</style>
