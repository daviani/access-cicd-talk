<template>
  <div class="wave-container">
    <svg
      class="waves"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 24 150 28"
      preserveAspectRatio="none"
      shape-rendering="auto"
    >
      <defs>
        <path
          id="wave"
          d="M-160 44c30 0 58-18 88-18s58 18 88 18 58-18 88-18 58 18 88 18 v44h-352z"
        />
      </defs>
      <g class="parallax">
        <use href="#wave" x="48" y="0" class="wave-1" />
        <use href="#wave" x="48" y="3" class="wave-2" />
        <use href="#wave" x="48" y="5" class="wave-3" />
        <use href="#wave" x="48" y="7" class="wave-4" />
      </g>
    </svg>
  </div>
</template>

<style scoped>
.wave-container {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 7vh;
  overflow: hidden;
  line-height: 0;
  z-index: 0;
}

.waves {
  width: 100%;
  height: 100%;
  min-height: 60px;
}

.wave-1 {
  fill: rgba(216, 222, 233, 0.7);
  animation: wave-move 25s cubic-bezier(0.36, 0.45, 0.63, 0.53) infinite;
}

.wave-2 {
  fill: rgba(216, 222, 233, 0.5);
  animation: wave-move 19s cubic-bezier(0.36, 0.45, 0.63, 0.53) -2s infinite;
}

.wave-3 {
  fill: rgba(229, 233, 240, 0.3);
  animation: wave-move 13s cubic-bezier(0.36, 0.45, 0.63, 0.53) -4s infinite;
}

.wave-4 {
  fill: rgba(229, 233, 240, 0.8);
  animation: wave-move 30s cubic-bezier(0.36, 0.45, 0.63, 0.53) -5s infinite;
}

@keyframes wave-move {
  0% {
    transform: translate3d(-90px, 0, 0);
  }
  100% {
    transform: translate3d(85px, 0, 0);
  }
}

@media (prefers-reduced-motion: reduce) {
  .wave-1, .wave-2, .wave-3, .wave-4 {
    animation: none;
  }
}
</style>
