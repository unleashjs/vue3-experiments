<template>
	<div :class="[
		`container-item container-item--${variant}`,
		'grid overflow-hidden',
		{
			'col-span-full': variant && variant !== 'contained',
			'[&>*]:col-[breakout]': variant === 'breakout',
			'[&>*]:col-[contained] [&>*]:col-start-[breakout]': variant === 'breakout-l',
			'[&>*]:col-[contained] [&>*]:col-end-[breakout]': variant === 'breakout-r',
			'[&>*]:col-[contained]': variant === 'full-contained',
			'[&>*]:col-[full]': variant === 'full',
			'col-[contained]': !variant || variant === 'contained',
			'grid-cols-[inherit]': variant && variant !== 'contained'
		}]"
	>
		<slot />
	</div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

export type ContainerVariant = 'contained' | 'breakout' | 'breakout-l' | 'breakout-r' | 'full' | 'full-contained' // TODO: extract to a separate ContainerVariant.ts file

export type Props = {
	variant?: ContainerVariant
}

defineProps<Props>()
</script>
