<script setup>
const props = defineProps({
  question: Object,
  selectedAnswer: Number,
});

const emit = defineEmits(["selectOption"]);

function emitSelectedOption(option) {
  emit("selectOption", option);
}

const labels = ["A", "B", "C", "D", "E", "F"];
</script>

<template>
  <section class="question-container">
    <p class="question-eyebrow">Pilih jawaban yang benar</p>
    <h1 class="question-title">{{ question.text }}</h1>
  </section>

  <section class="option-container">
    <div
      class="option"
      v-for="(option, index) in question.answers"
      :key="option.id"
      @click="emitSelectedOption(option)"
      :class="{ selected: selectedAnswer === option.id }"
    >
      <div class="option-label">{{ option.label || labels[index] }}</div>
      <div class="option-value">{{ option.text }}</div>
      <div class="option-check">
        <svg
          v-if="selectedAnswer === option.id"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="3"
          width="14"
          height="14"
        >
          <polyline points="20 6 9 17 4 12" />
        </svg>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@400;500;600;700&display=swap");

.question-container {
  margin-bottom: 32px;
}

.question-eyebrow {
  font-family: "Outfit", sans-serif;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: #334155;
  margin-bottom: 14px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.question-eyebrow::before {
  content: "";
  display: inline-block;
  width: 20px;
  height: 2px;
  background: #f97316;
  border-radius: 2px;
}

.question-title {
  font-family: "Outfit", sans-serif;
  font-size: 22px;
  font-weight: 700;
  color: #f1f5f9;
  line-height: 1.5;
  margin: 0;
}

/* Options */
.option-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.option {
  display: flex;
  align-items: center;
  cursor: pointer;
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.07);
  background: rgba(255, 255, 255, 0.03);
  transition: all 0.2s ease;
  position: relative;
  overflow: hidden;
}

.option::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    135deg,
    rgba(249, 115, 22, 0.05) 0%,
    transparent 60%
  );
  opacity: 0;
  transition: opacity 0.2s ease;
}

.option:hover {
  border-color: rgba(249, 115, 22, 0.3);
  background: rgba(249, 115, 22, 0.06);
  transform: translateX(4px);
}

.option:hover::before {
  opacity: 1;
}

.option-label {
  font-family: "Bebas Neue", cursive;
  font-size: 18px;
  min-width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: #334155;
  border-right: 1px solid rgba(255, 255, 255, 0.06);
  letter-spacing: 0.05em;
  transition: all 0.2s ease;
}

.option-value {
  font-family: "Outfit", sans-serif;
  font-size: 14px;
  font-weight: 500;
  padding: 0 20px;
  color: #94a3b8;
  flex: 1;
  height: 60px;
  display: flex;
  align-items: center;
  transition: color 0.2s ease;
}

.option-check {
  width: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  color: #f97316;
  opacity: 0;
  transition: opacity 0.2s ease;
}

/* Selected state */
.selected {
  border-color: rgba(249, 115, 22, 0.5) !important;
  background: rgba(249, 115, 22, 0.08) !important;
  transform: none !important;
  box-shadow:
    0 0 0 1px rgba(249, 115, 22, 0.2),
    inset 0 0 30px rgba(249, 115, 22, 0.04);
}

.selected .option-label {
  color: #f97316;
  border-right-color: rgba(249, 115, 22, 0.2);
}

.selected .option-value {
  color: #e2e8f0;
  font-weight: 600;
}

.selected .option-check {
  opacity: 1;
}
</style>
