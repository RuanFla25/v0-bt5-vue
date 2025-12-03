<template>
  <button class="btn btn-outline-secondary" @click="toggle" :title="t('theme.toggle')">
    <i :class="iconClass"></i>
  </button>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const theme = ref<'light' | 'dark'>('light');
const iconClass = ref('bi bi-sun');

function applyTheme() {
  document.documentElement.setAttribute('data-bs-theme', theme.value);
  iconClass.value = theme.value === 'dark' ? 'bi bi-moon' : 'bi bi-sun';
  localStorage.setItem('theme', theme.value);
}

onMounted(() => {
  const saved = localStorage.getItem('theme') as 'light' | 'dark' | null;
  if (saved) theme.value = saved;
  else if (window.matchMedia('(prefers-color-scheme: dark)').matches) theme.value = 'dark';
  applyTheme();
});

function toggle() {
  theme.value = theme.value === 'dark' ? 'light' : 'dark';
  applyTheme();
}
</script>
