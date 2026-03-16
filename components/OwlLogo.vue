<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 100 100"
    :width="size"
    :height="size"
    aria-hidden="true"
  >
    <g :fill="bodyColor">
      <path d="M50 8 L35 25 L30 22 L32 35 L25 38 L30 48 L20 55 L35 58 L35 75 L50 92 L65 75 L65 58 L80 55 L70 48 L75 38 L68 35 L70 22 L65 25 Z" />
      <circle cx="42" cy="45" r="8" :fill="eyeColor" />
      <circle cx="58" cy="45" r="8" :fill="eyeColor" />
      <circle cx="40" cy="43" r="3" />
      <circle cx="56" cy="43" r="3" />
      <path d="M40 60 L50 55 L60 60 L60 72 L50 80 L40 72 Z" :fill="eyeColor" />
      <path d="M46 62 L50 60 L54 62 L54 68 L50 72 L46 68 Z" />
    </g>
  </svg>
</template>

<script setup>
defineProps({
  size: { type: Number, default: 48 },
  bodyColor: { type: String, default: '#4C566A' },
  eyeColor: { type: String, default: '#ECEFF4' },
})
</script>