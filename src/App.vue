<template>
  <div class="app">
    <GenericCard>
      <!-- De header van de card -->
      <GenericCardHeader>
        <h2>Your access code:</h2>

        <button>
          <X />
        </button>
      </GenericCardHeader>

      <DigitOverview>
        <DigitSingle
          v-for="(digit, index) in code"
          :key="index"
          :value="digit"
          :loading="loading"
        />
      </DigitOverview>

      <!-- Footer van de card component -->
      <GenericCardFooter>
        <button @click="getCode" class="btn">Get new Code</button>

        <p>
          Your access code is unique for your apartment. If you generate a new code, the old code
          can not be used anymore.
        </p>
      </GenericCardFooter>
    </GenericCard>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { X } from 'lucide-vue-next'
import DigitOverview from '@/components/digit/DigitOverview.vue'
import DigitSingle from '@/components/digit/DigitSingle.vue'
import GenericCard from '@/components/generic/GenericCard.vue'
import GenericCardFooter from '@/components/generic/GenericCardFooter.vue'
import GenericCardHeader from '@/components/generic/GenericCardHeader.vue'

const code = ref(['*', '*', '*', '*'])
const loading = ref(true)

const getCode = async () => {
  loading.value = true
  code.value = ['*', '*', '*', '*']

  code.value = await fetch('https://mct-marty.be/happy-home/').then((res) => res.json())
  loading.value = false
}

getCode()
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --page-background: #0f0081;
}

html,
body {
  background-color: var(--page-background);
  font-family: Inter, sans-serif;
}

.app {
  display: grid;
  place-items: center;
  min-height: 100vh;
}

.btn {
  padding: 1rem 1rem;
  border: none;
  font-weight: bold;
  border-radius: 0.5rem;
  background-color: #3014ff;
  color: #fff;
  width: 100%;
  cursor: pointer;
  margin-bottom: 0.75rem;
}

.btn:hover {
  background-color: #0056b3;
}
</style>
