<script setup lang="ts">
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

// Use `defineProps` with `v-model` support
const props = defineProps<{
  height?: number;
  weight?: number;
}>();

// Emits for `v-model` and actions
const emits = defineEmits<{
  (e: "update:height", value: number | undefined): void;
  (e: "update:weight", value: number | undefined): void;
  (e: "calculate"): void;
  (e: "reset"): void;
}>();

// Helper function to update number props
const updateHeight = (value: string) =>
  emits("update:height", value ? Number(value) : undefined);
const updateWeight = (value: string) =>
  emits("update:weight", value ? Number(value) : undefined);
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
        :value="props.height"
        @input="updateHeight($event.target.value)"
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
        :value="props.weight"
        @input="updateWeight($event.target.value)"
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
