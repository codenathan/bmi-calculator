<script setup lang="ts">
import BmiForm from "@/components/BmiForm.vue";
import BmiResult from "@/components/BmiResult.vue";
import { ref } from "vue";
import { Calculator } from "lucide-vue-next";

import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";

import type { BMIResult } from "@/types/bmi";

const height = ref<number | undefined>(undefined);
const weight = ref<number | undefined>(undefined);
const result = ref<BMIResult | null>(null);

const handleReset = () => {
  height.value = undefined;
  weight.value = undefined;
  result.value = null;
};

const calculateBMI = (heightCm: number, weightKg: number): BMIResult => {
  const heightM = heightCm / 100;
  const bmi = weightKg / (heightM * heightM);
  let category = "";
  let color = "";

  if (bmi < 18.5) {
    category = "Underweight";
    color = "text-blue-500";
  } else if (bmi >= 18.5 && bmi < 24.9) {
    category = "Normal weight";
    color = "text-green-500";
  } else if (bmi >= 25 && bmi < 29.9) {
    category = "Overweight";
    color = "text-yellow-500";
  } else {
    category = "Obese";
    color = "text-red-500";
  }

  return {
    bmi: parseFloat(bmi.toFixed(1)),
    category,
    color,
  };
};

const handleCalculate = () => {
  if (height.value && weight.value) {
    result.value = calculateBMI(height.value, weight.value);
  }
};
</script>

<template>
  <Card
    class="w-full max-w-md shadow-lg border-2 transition-all duration-300 hover:shadow-xl"
  >
    <CardHeader class="space-y-1 pb-6">
      <div class="flex items-center gap-2">
        <div class="p-2 rounded-lg bg-primary/10">
          <Calculator class="h-6 w-6 text-primary" />
        </div>
        <CardTitle class="text-2xl font-bold">BMI Calculator</CardTitle>
      </div>
      <CardDescription>
        Calculate your Body Mass Index to assess your health
      </CardDescription>
    </CardHeader>

    <CardContent class="space-y-6">
      <BmiForm
        v-model:height="height"
        v-model:weight="weight"
        @calculate="handleCalculate"
        @reset="handleReset"
      />

      <BmiResult v-if="result" :result="result" />
    </CardContent>
  </Card>
</template>
