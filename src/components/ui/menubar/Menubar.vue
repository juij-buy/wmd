<script setup lang="ts">
import {
  MenubarRoot,
  type MenubarRootEmits,
  type MenubarRootProps,
  useForwardPropsEmits,
} from 'radix-vue'
import { computed, type HTMLAttributes } from 'vue'
import { cn } from '@/lib/utils'

const props = defineProps<MenubarRootProps & { class?: HTMLAttributes[`class`] }>()
const emits = defineEmits<MenubarRootEmits>()

const delegatedProps = computed(() => {
  const { class: _, ...delegated } = props

  return delegated
})

const forwarded = useForwardPropsEmits(delegatedProps, emits)
</script>

<template>
  <MenubarRoot
    v-bind="forwarded"
    :class="
      cn(
        'flex h-10 items-center gap-x-1 rounded-md border bg-background p-1',
        props.class,
      )
    "
  >
    <slot />
  </MenubarRoot>
</template>
