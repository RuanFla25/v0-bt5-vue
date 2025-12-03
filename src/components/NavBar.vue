<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">{{ $t('app.name') }}</router-link>

      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarContent">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li v-for="route in menuRoutes" :key="route.path" class="nav-item">
            <RouterLink class="nav-link" :to="route.path">
              {{ $t(route.meta.titleKey) }}
            </RouterLink>
          </li>
        </ul>

        <ThemeToggle />
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { useRouter } from 'vue-router';
import ThemeToggle from './ThemeToggle.vue';

const router = useRouter();

const menuRoutes = computed(() =>
  router.getRoutes().filter(r => r.meta && r.meta.titleKey)
);
</script>
