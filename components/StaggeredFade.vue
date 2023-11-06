<template>
  <TransitionGroup
    name="staggered-fade"
    :css="false"
    appear
    @before-enter="onBeforeEnter"
    @enter="onEnter"
  >
    <slot />
  </TransitionGroup>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { watchAtMost } from '@vueuse/core'
import { useMotion } from '@vueuse/motion'

export type Props = {
	duration?: number
	dataTag?: string
	variantOnDone?: string
}

const props = withDefaults(defineProps<Props>(), {
	duration: 100,
	dataTag: 'sfi',
	variantOnDone: 'permanent'
})

const dataTag = computed(() => 'data-' + props.dataTag)

/**
 * Check if the user prefers reduced motion
 */
function prefersReducedMotion() {
	const mediaQueryList = window.matchMedia('(prefers-reduced-motion: reduce)')
	return mediaQueryList.matches
}

/**
 * Get all items to transition
 * @param el The element to transition
 */
function getItems(el: Element | HTMLElement) {
	const items: HTMLElement[] = [...el.querySelectorAll<HTMLElement>(`[${dataTag.value}]`)]
	if (el.getAttribute(dataTag.value)) items.unshift(el as HTMLElement)
	return items
}

/**
 * Hide all items before entering
 * @param el The element to transition
 */
function onBeforeEnter(el: Element) {
	if (prefersReducedMotion()) return

	for (const item of getItems(el)) {
		item.style.opacity = '0'
		item.style.visibility = 'hidden'
	}
}

/**
 * Animate all items on enter
 * @param el The element to transition
 */
function onEnter(el: Element) {
	if (prefersReducedMotion()) return

	const items = getItems(el)
	for (let i = 0; i < items.length; i++) {
		animateElement(items[i], i)
	}
}

function animateElement(el: HTMLElement, dynamicOrder: number) {
	const index = el.getAttribute(dataTag.value) || dynamicOrder
	const delay = (~~index + 1) * props.duration

	setTimeout(() => {
		const motion = useMotion(el, {
			initial: {
				opacity: 0,
				y: 35,
				visibility: 'visible'
			},
			visibleOnce: {
				opacity: 1,
				y: 0,
				transition: {
					type: 'spring',
					stiffness: 125,
					damping: 25,
					mass: 1
				}
			},
			permanent: {
				opacity: 1,
				y: 0
			}
		})

		watchAtMost(
			() => motion.isAnimating.value,
			() => {
				// Apply the permanent variant to elements that are outside the viewport
				if (props.variantOnDone && !motion.isAnimating.value) {
					motion.apply(props.variantOnDone)
				}
			}, {
				count: 3
			}
		)
	}, delay)
}
</script>
