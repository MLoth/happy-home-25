<template>
  <span :class="['digit-single', { 'digit-single--loading': loading }]">{{ value }}</span>
</template>

<script setup>
defineProps({
  value: {
    type: String,
    required: true,
  },
  loading: {
    type: Boolean,
    default: false,
  },
})
</script>

<style scoped>
@keyframes loading {
  0% {
    opacity: 0.2;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0.2;
  }
}

.digit-single {
  flex: 1;
  text-align: center;
  background-color: #f6f6f6;
  font-size: 3rem;
  padding: 0.5rem 0;
  border-radius: 0.5rem;
  font-weight: bold;
  color: #222;
}
.digit-single--loading {
  animation: loading 3s infinite;
}
</style>
