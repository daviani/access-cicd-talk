<template>
  <footer
    v-if="$nav.currentLayout !== 'cover'"
    class="absolute bottom-0 left-0 right-0 flex items-center justify-between px-6 pb-3"
    style="z-index: 50;"
  >
    <OwlLogo :size="28" body-color="#4C566A" eye-color="#ECEFF4"></OwlLogo>
    <span class="text-xs font-medium" style="color: #4C566A;">
      {{ $nav.currentPage }} / {{ $nav.total }}
    </span>
  </footer>
</template>