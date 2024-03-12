<script setup>
  import { useMonitor } from '@/composables/monitor';

  const { menu } = useMonitor();
</script>

<template>
  <div>
    <component :is="menu" />
    <main>
      <router-view />
    </main>
  </div>
</template>