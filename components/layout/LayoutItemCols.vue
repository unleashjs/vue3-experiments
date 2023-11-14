<template>
	<div
		class="layout-item-cols md:grid-flow-col
					[&>*:first-child]:before:absolute [&>*:first-child]:before:inset-0 [&>*:first-child]:before:col-start-1 [&>*:first-child]:before:col-end-3 [&>*:first-child]:before:bg-inherit [&>*:first-child]:before:z-[-1]
					[&>*:last-child]:before:absolute [&>*:last-child]:before:inset-0 [&>*:last-child]:before:col-start-4 [&>*:last-child]:before:col-end-6 [&>*:last-child]:before:bg-inherit [&>*:last-child]:before:z-[-1]"
	>
		<slot />
	</div>
</template>

<style>
.layout-item-cols {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
	grid-template-rows: 1fr;
}

.auto-cols-fr > *:first-child:nth-last-child(2) {
	width: calc(var(--col-width) * 2%);
}

.layout-item-cols > *:first-child:nth-last-child(3),
.layout-item-cols > *:first-child:nth-last-child(3) ~ .layout-item-cols > :first-child {
	width: calc(var(--col-width) * 3%);
}

.layout-item-cols > *:first-child:nth-last-child(3) {
	width: 40%;
}
</style>
