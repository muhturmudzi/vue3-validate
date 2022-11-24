<template>
  <Topbar />

  <main>
    <router-view></router-view>
  </main>
</template>

<script setup>
  import Topbar from '@/components/Topbar.vue'
</script>