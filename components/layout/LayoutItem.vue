<template>
	<div
		class="layout-item grid col-span-full md:relative"
		:class="{
			'[&>*]:col-[breakout]': variant === 'breakout',
			'[&>*]:col-[contained] [&>*]:col-start-[breakout]': variant === 'breakout-l',
			'[&>*]:col-[contained] [&>*]:col-end-[breakout]': variant === 'breakout-r',
			'[&>*]:col-[contained]': variant === 'full-contained',
			'[&>*]:col-[full]': variant === 'full',
			'col-[contained]': !variant || variant === 'contained',
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
