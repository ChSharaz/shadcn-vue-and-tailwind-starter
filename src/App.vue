<template>
  <div class="b p-4 min-h-screen">
    <div class="py-2">
      <div class="container">
        <router-view></router-view>
      </div>
    </div>
    <div class="container mt-20 max-w-[500px]">
      <h1 class="text-center mb-10 text-4xl font-bold">Login</h1>
      <Example />
    </div>
  </div>
</template>

<script setup>
import Example from '@/components/base/Example.vue'
</script>
z
