<script setup>
defineProps({
  currentQuestionIndex: Number,
  totalQuestions: Number,
  allAnswered: Boolean,
});

const emit = defineEmits(["next", "prev", "finish"]);
</script>

<template>
  <div class="navigation">
    <button
      class="btn btn-prev"
      @click="emit('prev')"
      :disabled="currentQuestionIndex <= 0"
    >
      <svg
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2.5"
        width="15"
        height="15"
      >
        <path d="M19 12H5M12 5l-7 7 7 7" />
      </svg>
      <span class="btn-label">Prev</span>
    </button>

    <div class="dot-nav">
      <div
        v-for="n in Math.min(totalQuestions, 8)"
        :key="n"
        class="dot"
        :class="{
          'dot-active': n - 1 === currentQuestionIndex,
          'dot-done': n - 1 < currentQuestionIndex,
        }"
      ></div>
      <span v-if="totalQuestions > 8" class="dot-more"
        >+{{ totalQuestions - 8 }}</span
      >
    </div>

    <div class="right-btns">
      <button
        class="btn btn-next"
        @click="emit('next')"
        :disabled="currentQuestionIndex >= totalQuestions - 1"
      >
        <span class="btn-label">Next</span>
        <svg
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2.5"
          width="15"
          height="15"
        >
          <path d="M5 12h14M12 5l7 7-7 7" />
        </svg>
      </button>

      <button
        class="btn btn-finish"
        @click="emit('finish')"
        :disabled="!allAnswered"
      >
        <svg viewBox="0 0 24 24" fill="currentColor" width="14" height="14">
          <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z" />
        </svg>
        <!-- Sembunyikan teks "Selesai" di layar sangat kecil, icon saja -->
        <span class="btn-label">Selesai</span>
      </button>
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@400;500;600;700&display=swap");

.navigation {
  margin-top: 40px;
  padding-top: 28px;
  border-top: 1px solid rgba(255, 255, 255, 0.06);
  display: flex;
  align-items: center;
  gap: 16px;
  justify-content: space-between;
}

.btn {
  font-family: "Outfit", sans-serif;
  font-size: 13px;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 11px 20px;
  border-radius: 12px;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
  letter-spacing: 0.03em;
  white-space: nowrap;
}

.btn:disabled {
  opacity: 0.25;
  cursor: not-allowed;
  transform: none !important;
}

.btn-prev {
  background: rgba(255, 255, 255, 0.05);
  color: #64748b;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.btn-prev:hover:not(:disabled) {
  background: rgba(255, 255, 255, 0.08);
  color: #94a3b8;
  transform: translateX(-2px);
}

/* Dot nav */
.dot-nav {
  display: flex;
  align-items: center;
  gap: 6px;
  flex: 1;
  justify-content: center;
}

.dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.2s ease;
}

.dot-active {
  background: #f97316;
  width: 20px;
  border-radius: 3px;
  box-shadow: 0 0 8px rgba(249, 115, 22, 0.6);
}

.dot-done {
  background: rgba(249, 115, 22, 0.4);
}

.dot-more {
  font-family: "Outfit", sans-serif;
  font-size: 11px;
  color: #334155;
  margin-left: 2px;
}

/* Right buttons group */
.right-btns {
  display: flex;
  gap: 10px;
  align-items: center;
}

.btn-next {
  background: rgba(255, 255, 255, 0.07);
  color: #e2e8f0;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.btn-next:hover:not(:disabled) {
  background: rgba(255, 255, 255, 0.1);
  transform: translateX(2px);
}

.btn-finish {
  background: linear-gradient(135deg, #f97316, #fbbf24);
  color: #0a0a0f;
  font-weight: 700;
  box-shadow: 0 4px 16px rgba(249, 115, 22, 0.35);
}

.btn-finish:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(249, 115, 22, 0.5);
}

/* Tambahkan di bagian bawah <style scoped> */

/* Tablet */
@media (max-width: 640px) {
  .navigation {
    gap: 10px;
    margin-top: 24px;
    padding-top: 20px;
  }

  .btn {
    padding: 9px 14px;
    font-size: 12px;
    border-radius: 10px;
  }

  .right-btns {
    gap: 8px;
  }

  .dot {
    width: 5px;
    height: 5px;
  }

  .dot-active {
    width: 16px;
  }
}

/* Mobile kecil */
@media (max-width: 400px) {
  .navigation {
    flex-wrap: wrap;
    gap: 8px;
  }

  .btn {
    padding: 8px 12px;
    font-size: 11px;
    gap: 5px;
  }

  /* Sembunyikan teks, tampilkan icon saja pada btn-finish di mobile kecil */
  .btn-finish .btn-label {
    display: none;
  }

  .dot-nav {
    order: -1; /* pindah dot ke baris atas */
    flex: 0 0 100%; /* full width */
    justify-content: center;
    margin-bottom: 4px;
  }
}
</style>
