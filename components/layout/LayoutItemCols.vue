<template>
	<div class="layout-item-cols grid md:grid-flow-col">
		<slot />
	</div>
</template>

<style>
.layout-item-cols > * {
	@apply relative md:static;
}

.layout-item-cols > *::before {
	content: '';
	@apply absolute inset-0 -mx-[var(--edge-padding)] bg-inherit pointer-events-none z-[-1]
		first:col-start-[full] first:col-end-[contained]
		last:col-start-[contained] last:col-end-[full]
		md:mx-0 md:hidden md:first:block md:last:block;
}

.auto-cols-fr > *:first-child:nth-last-child(2) {
	width: calc(var(--col-width) * 2%);
}
</style>
