<script setup lang="ts">
import BmiCalculator from "@/components/BmiCalculator.vue";

</script>

<template>
  <div
    class="min-h-screen from-background via-background to-secondary/20 flex items-center justify-center p-4"
  >
    <div class="w-full max-w-7xl mx-auto">
      <div class="text-center mb-8 space-y-3">
        <h1
          class="text-4xl md:text-5xl font-bold text-foreground tracking-tight"
        >
          Health Check
        </h1>
        <p class="text-lg text-muted-foreground max-w-2xl mx-auto">
          Monitor your body mass index to maintain a healthy lifestyle
        </p>
      </div>

      <div class="flex justify-center">
        <BmiCalculator />
      </div>
    </div>
  </div>
</template>
