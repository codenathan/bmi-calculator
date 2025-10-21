<script setup lang="ts">
import {
  Card,
  CardContent,
  CardDescription,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";

import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";

import { Calculator, TrendingUp } from "lucide-vue-next";
import { ref } from "vue";

interface BMIResult {
  bmi: number;
  category: string;
  color: string;
}

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
            <div class="space-y-4">
              <div class="space-y-2">
                <Label htmlFor="height" class="text-sm font-medium">
                  Height (cm)
                </Label>
                <Input
                  id="height"
                  type="number"
                  placeholder="Enter height in centimeters"
                  class="transition-all duration-200 focus:scale-[1.01]"
                  v-model="height"
                />
              </div>

              <div class="space-y-2">
                <Label htmlFor="weight" class="text-sm font-medium">
                  Weight (kg)
                </Label>
                <Input
                  id="weight"
                  type="number"
                  placeholder="Enter weight in kilograms"
                  class="transition-all duration-200 focus:scale-[1.01]"
                  v-model="weight"
                />
              </div>
            </div>

            <div class="flex gap-3">
              <Button
                class="flex-1 transition-all duration-200 hover:scale-[1.02]"
                :disabled="!height || !weight"
                @click="handleCalculate"
              >
                Calculate
              </Button>

              <Button
                variant="outline"
                class="transition-all duration-200 hover:scale-[1.02]"
                @click="handleReset"
              >
                Reset
              </Button>
            </div>

            <div
              v-if="result"
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
                  BMI ranges: Underweight (&lt;18.5) • Normal (18.5-24.9) •
                  Overweight (25-29.9) • Obese (≥30)
                </p>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
  </div>
</template>
