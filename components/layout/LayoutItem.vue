<template>
	<div
		class="grid col-span-full relative [&>*]:grid"
		:class="{
			'[&>*]:col-start-2 [&>*]:col-end-5': variant === 'breakout',
			'[&>*]:col-start-2 [&>*]:col-end-4': variant === 'breakout-l',
			'[&>*]:col-start-3 [&>*]:col-end-5': variant === 'breakout-r',
			'[&>*]:col-start-3 [&>*]:col-end-4': variant === 'full-contained',
			'[&>*]:col-span-full': variant === 'full',
			'col-start-3 col-end-4': !variant || variant === 'contained',
			'grid-cols-[inherit]': variant && variant !== 'contained'
		}"
	>
		<slot />
	</div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

export type LayoutVariant = 'contained' | 'breakout' | 'breakout-l' | 'breakout-r' | 'full' | 'full-contained' // TODO: extract to a separate LayoutVariant.ts file

export type Props = {
	variant?: LayoutVariant
}

defineProps<Props>()
</script>
