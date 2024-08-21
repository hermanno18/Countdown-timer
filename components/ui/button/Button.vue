<script setup lang="ts">
import type { HTMLAttributes } from 'vue'
import { Primitive, type PrimitiveProps } from 'radix-vue'
import { type ButtonVariants, buttonVariants } from '.'
import { cn } from '@/lib/utils'

interface Props extends PrimitiveProps {
  variant?: ButtonVariants['variant']
  size?: ButtonVariants['size']
  class?: HTMLAttributes['class']
}

const props = withDefaults(defineProps<Props>(), {
  as: 'button',
})

const animateSlotToUp = (e: MouseEvent) => {
  const target = e.currentTarget as HTMLElement;
  const defaultSlot = target.querySelector("#default");
  const activeSlot = target.querySelector("#active");

  if (!defaultSlot || !activeSlot) return;
  useGsap.to(defaultSlot, {
    y: '-100%',
    scale: 0.5,
    duration: 0.3
  }); 
  
  useGsap.to(activeSlot, {
    y: '-100%',
    height: "fit-content",
    scale: 1,
  })
  useGsap.to(target, {
    scale: 1.05,
  })
}
const animateSlotToDown = (e: MouseEvent) => {
  const target = e.currentTarget as HTMLElement;
  const defaultSlot = target.querySelector("#default");
  const activeSlot = target.querySelector("#active");

  if (!defaultSlot || !activeSlot) return;
  useGsap.to(defaultSlot, {
    scale: 1,
    y: 0,
    duration: 0.5
  })
  useGsap.to(activeSlot, {
    y: 0,
    scale: 0.5,
  })
  useGsap.to(target, {
    scale: 1,
  })
}

onMounted(() => {
})

</script>

<template>
  <Primitive @mouseover="animateSlotToUp" @mouseleave="animateSlotToDown" :as="as" :as-child="asChild"
    class="flex" :class="cn(buttonVariants({ variant, size }), props.class)">
    <div class=" relative overflow-clip flex-1">
      <div id="default" >
        <slot />
      </div>
      <div id="active" class="absolute uppercase w-full">
        <slot />
      </div>
    </div>
  </Primitive>
</template>
