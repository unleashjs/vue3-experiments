<template>
	<div :class="[
		`container-cols grid grid-flow-row-dense [&>*]:relative`,
		{
			'container-cols--1 grid-cols-1': !cols || cols === 1,
			'container-cols--2 md:grid-cols-2': cols === 2,
			'container-cols--3 md:grid-cols-3': cols === 3,
			'container-cols--4 md:grid-cols-2 lg:grid-cols-4': cols === 4
		}]"
	>
		<slot />
	</div>
</template>

<script setup lang="ts">
export type Props = {
	cols?: 1 | 2 | 3 | 4
}

defineProps<Props>()
</script>

<style scoped>
.container-cols > :deep(*::before) {
	content: '';
	@apply absolute inset-0 -mx-[var(--edge-padding)] bg-inherit z-[-1] md:mx-0 md:hidden;
}

/* Left side background */
.container-cols--2 > :deep(*::before:nth-child(2n+1)),
.container-cols--3 > :deep(*::before:nth-child(3n+1)),
.container-cols--4 > :deep(*::before:nth-child(2n+1)), /* tablet view for 4 cols */
.container-cols--4 > :deep(*::before:nth-child(4n+1)) {
	@apply md:-left-[100vw] md:right-full block;
}

/* Right side background */
.container-cols--2 > :deep(*::before:nth-child(2n+2)),
.container-cols--3 > :deep(*::before:nth-child(3n+3)),
.container-cols--4 > :deep(*::before:nth-child(2n+2)), /* tablet view for 4 cols */
.container-cols--4 > :deep(*::before:nth-child(4n+4)) {
	@apply md:w-[100vw] md:left-full block;
}

/* Hide background for middle items */
.container-cols--4 > :deep(*::before:nth-child(2n+1):not(:nth-child(4n+1))),
.container-cols--4 > :deep(*::before:nth-child(2n+2):not(:nth-child(4n+4))) {
	@apply lg:hidden;
}

/* Breakout left exceptions TODO */
.container-item--breakout-l > .container-cols--2 {
	grid-template-columns: minmax(0, calc(var(--breakout-max-width) / 2)) minmax(0, 1fr);
}

.container-item--breakout-l > .container-cols--3 {
	grid-template-columns: repeat(3, minmax(0, calc(var(--breakout-max-width) / 1)));
}

.container-item--breakout-l > .container-cols--4 {
	grid-template-columns: repeat(2, minmax(0, calc(var(--breakout-max-width) / 4))) repeat(2, minmax(0, 1fr));
}

/* Breakout right exceptions TODO */
.container-item--breakout-r > .container-cols--2 {
	grid-template-columns: minmax(0, 1fr) minmax(0, calc(var(--breakout-max-width) / 2));
}

.container-item--breakout-r > .container-cols--3 {
	grid-template-columns: repeat(2, minmax(0, 1fr)) minmax(0, calc(var(--breakout-max-width) / 3)); /* TODO */
}

.container-item--breakout-r > .container-cols--4 {
	grid-template-columns: repeat(2, minmax(0, 1fr)) repeat(2, minmax(0, calc(var(--breakout-max-width) / 4)));
}
</style>
