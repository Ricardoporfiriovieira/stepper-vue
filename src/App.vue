<template>
<StepProgress :data="dataSteps" ref="stepProgress" ></StepProgress>

<div>
  <button @click="stepProgress.previousStep">Anterior</button>
  <button @click="stepProgress.nextStep">Proximo</button>
</div>

</template>

<script setup>

import { ref } from 'vue';

import StepProgress from './components/StepProgress.vue'


const stepProgress = ref();

const dataSteps = {
  steps: ['Step 1', 'Step 2', 'Step 3'],
  currentStep: 1,
  activeColor: '#65a30d',
  passiveColor: '#84cc16'
};

</script>

<style>

</style>
