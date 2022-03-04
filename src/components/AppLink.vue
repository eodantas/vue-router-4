<script setup>
import { computed } from 'vue'
import { RouterLink } from 'vue-router'
const props = defineProps({
  ...RouterLink.props
})
const isExternal = computed(
  () => typeof props.to === 'string' && props.to.startsWith('http')
)
</script>
<template>
  <a
    v-if="isExternal"
    :href="props.to"
    target="_blank"
    rel="noopener"
    class="external-link"
  >
    <slot />
  </a>
  <RouterLink v-else v-bind="props" class="internal-link"><slot /></RouterLink>
</template>
