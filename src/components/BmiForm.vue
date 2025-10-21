<script setup lang="ts">
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

const props = defineProps<{
  height?: number;
  weight?: number;
}>();

const emits = defineEmits<{
  (e: "calculate"): void;
  (e: "reset"): void;
}>();

const heightModel = defineModel<number | undefined>("height");
const weightModel = defineModel<number | undefined>("weight");
</script>

<template>
  <div class="space-y-4">
    <!-- Height input -->
    <div class="space-y-2">
      <Label htmlFor="height" class="text-sm font-medium">Height (cm)</Label>
      <Input
        id="height"
        type="number"
        placeholder="Enter height in centimeters"
        class="transition-all duration-200 focus:scale-[1.01]"
        v-model="heightModel"
      />
    </div>

    <!-- Weight input -->
    <div class="space-y-2">
      <Label htmlFor="weight" class="text-sm font-medium">Weight (kg)</Label>
      <Input
        id="weight"
        type="number"
        placeholder="Enter weight in kilograms"
        class="transition-all duration-200 focus:scale-[1.01]"
        v-model="weightModel"
      />
    </div>
  </div>

  <!-- Buttons -->
  <div class="flex gap-3 mt-4">
    <Button
      class="flex-1 transition-all duration-200 hover:scale-[1.02]"
      :disabled="!props.height || !props.weight"
      @click="emits('calculate')"
    >
      Calculate
    </Button>

    <Button
      variant="outline"
      class="transition-all duration-200 hover:scale-[1.02]"
      @click="emits('reset')"
    >
      Reset
    </Button>
  </div>
</template>
