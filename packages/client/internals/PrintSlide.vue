<script setup lang="ts">
import type { SlideRoute } from '@slidev/types'
import { useFixedNav, useNav } from '../composables/useNav'
import { createFixedClicks } from '../composables/useClicks'
import PrintSlideClick from './PrintSlideClick.vue'

const { route } = defineProps<{ route: SlideRoute }>()
const { isPrintWithClicks } = useNav()
const clicks0 = createFixedClicks(route, 0, () => !isPrintWithClicks.value)
</script>

<template>
  <PrintSlideClick
    :clicks-context="clicks0"
    :nav="useFixedNav(route, clicks0)"
  />
  <template v-if="!clicks0.disabled">
    <PrintSlideClick
      v-for="i of clicks0.total"
      :key="i"
      :nav="useFixedNav(route, createFixedClicks(route, i))"
    />
  </template>
</template>
