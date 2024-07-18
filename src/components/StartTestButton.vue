<script setup lang="ts">
import { RouterLink } from 'vue-router';

withDefaults(
  defineProps<{
    theme: 'filled' | 'outlined',
  }>(),
  {
    theme: 'filled',
  },
)
</script>

<template>
  <RouterLink to="/quiz">
    <button class="btn" :class="theme">
      пройти тест
    </button>
  </RouterLink>
</template>

<style scoped>
.btn {
  width: auto;
  border-radius: 9999px;
  text-transform: uppercase;
  padding-top: 0.75rem;
  padding-bottom: 0.75rem;
  padding-left: 2rem;
  padding-right: 2rem;
  font-family: "Merriweather", serif;
  font-weight: bold;
  letter-spacing: 0.0625rem;
}

.filled {
  background-color: var(--accent);
}

.outlined {
  border: 1px solid #fff;
  background-color: transparent;
  color: #fff;
}
</style>

