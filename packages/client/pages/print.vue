<script setup lang="ts">
import { watchEffect } from 'vue'
import { windowSize } from '../state'
import PrintContainer from '../internals/PrintContainer.vue'
import PrintStyle from '../internals/PrintStyle.vue'
import { useNav } from '../composables/useNav'

const { isPrintMode } = useNav()

watchEffect(() => {
  if (isPrintMode)
    (document.body.parentNode as HTMLElement).classList.add('print')
  else
    (document.body.parentNode as HTMLElement).classList.remove('print')
})
</script>

<template>
  <PrintStyle v-if="isPrintMode" />
  <div id="page-root" class="grid grid-cols-[1fr_max-content]">
    <PrintContainer
      class="w-full h-full"
      :style="{ background: 'var(--slidev-slide-container-background, black)' }"
      :width="windowSize.width.value"
    />
  </div>
</template>

<style lang="postcss">
html.print,
html.print body,
html.print #app {
  height: auto;
  overflow: auto;
}
html.print #page-root {
  height: auto;
  overflow: hidden;
}
html.print * {
  -webkit-print-color-adjust: exact;
}
html.print {
  width: 100%;
  height: 100%;
  overflow: visible;
}
html.print body {
  margin: 0 auto;
  border: 0;
  padding: 0;
  float: none;
  overflow: visible;
}
</style>
