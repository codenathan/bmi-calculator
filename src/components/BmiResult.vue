<script setup lang="ts">
import { TrendingUp } from "lucide-vue-next";

import type { BMIResult } from "@/types/bmi";

defineProps<{
  result: BMIResult;
}>();
</script>

<template>
  <div
    class="mt-6 p-6 bg-muted/50 rounded-lg space-y-3 animate-in fade-in-50 slide-in-from-bottom-3 duration-300"
  >
    <div class="flex items-center gap-2 text-muted-foreground">
      <TrendingUp class="h-4 w-4" />
      <span class="text-sm font-medium">Your Result</span>
    </div>

    <div class="space-y-2">
      <div class="flex items-baseline gap-2">
        <span class="text-4xl font-bold text-foreground">
          {{ result.bmi }}
        </span>
        <span class="text-sm text-muted-foreground">BMI</span>
      </div>
      <p :class="['text-lg font-semibold', result.color]">
        {{ result.category }}
      </p>
    </div>

    <div class="pt-3 border-t border-border/50">
      <p class="text-xs text-muted-foreground">
        BMI ranges: Underweight (&lt;18.5) • Normal (18.5-24.9) • Overweight
        (25-29.9) • Obese (≥30)
      </p>
    </div>
  </div>
</template>
