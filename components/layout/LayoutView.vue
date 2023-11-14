<template>
  <div class="col-grid grid pb-16">
	  <template v-for="([variant, label]) in Object.entries(VARIANTS)" :key="variant">
		  <LayoutItem>
			  <h2 class="text-3xl mt-16 mb-4 py-4 text-center border-y-2 border-dashed border-black">
				  {{ label }}
				  <br />
				  <small class="text-gray-500 text-sm">variant="{{ variant }}"</small>
			  </h2>
		  </LayoutItem>

		  <!-- LayoutItem with any child element -->
		  <LayoutItem :variant="variant as any">
			  <!-- Placeholder content -->
			  <img src="https://picsum.photos/2600/500" alt="Image" />
			  <p class="pt-3">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eros nunc, luctus id finibus eu, rhoncus vel diam. Fusce nec mi non neque accumsan sollicitudin. Vivamus ac vehicula nunc. Duis vehicula vulputate vulputate. Donec nec tempor metus. Sed consequat libero nec leo fermentum, ac tempor mauris semper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Donec consequat, arcu in iaculis gravida, lectus mi faucibus neque, id malesuada lacus eros eget sem. Integer facilisis bibendum dolor eget ornare. Suspendisse potenti.</p>
			  <p class="py-3">ALorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eros nunc, luctus id finibus eu, rhoncus vel diam. Fusce nec mi non neque accumsan sollicitudin. Vivamus ac vehicula nunc. Duis vehicula vulputate vulputate. Donec nec tempor metus. Sed consequat libero nec leo fermentum, ac tempor mauris semper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Donec consequat, arcu in iaculis gravida, lectus mi faucibus neque, id malesuada lacus eros eget sem. Integer facilisis bibendum dolor eget ornare. Suspendisse potenti.</p>
		  </LayoutItem>

		  <!-- LayoutItem with columns -->
		  <LayoutItem :variant="variant as any">
			  <LayoutItemCols>
				  <!-- Placeholder content -->
				  <!-- Supports background colors on each column -->
				  <div class="bg-orange-200 text-center font-bold py-16">Left</div>
				  <div class="bg-violet-300 text-center font-bold py-16">Right</div>
				  <div class="bg-violet-300 text-center font-bold py-16">Right</div>
			  </LayoutItemCols>
		  </LayoutItem>
	  </template>
  </div>
</template>

<style>
:root {
	--edge-padding: 2rem;
	--contained-max-width: 75rem;
	--breakout-max-width: 90rem;
	--contained-width: min(100% - (var(--edge-padding) * 2), var(--contained-max-width));
	--breakout-width: minmax(0, calc((var(--breakout-max-width) - var(--contained-max-width)) / 2));
	--full-width: minmax(var(--edge-padding), 1fr);
	--col-width: calc((var(--breakout-width) - var(--contained-width)) / 2)
}
</style>

<style scoped>
.col-grid {
	grid-template-columns:
		[full-start] var(--full-width)
		[breakout-start] var(--breakout-width)
		[contained-start] var(--contained-width) [contained-end]
		var(--breakout-width) [breakout-end]
		var(--full-width) [full-end];
}

/**
 * Columns
 */
/*[data-variant="breakout-l"] > .grid-flow-col > *:first-child:nth-last-child(2),
[data-variant="breakout-l"] > .grid-flow-col > *:first-child:nth-last-child(2) ~ [data-variant="breakout-l"] > .grid-flow-col > :first-of-type {
	width: 50%;
}
*/
</style>

<script setup lang="ts">
import LayoutItemCols from "@/views/LayoutItemCols.vue";
import LayoutItem from "@/views/LayoutItem.vue";

const VARIANTS = {
	contained: 'Contained (default)',
	breakout: 'Breakout',
	'breakout-l': 'Breakout left',
	'breakout-r': 'Breakout right',
	full: 'Full width',
	'full-contained': 'Full width contained',
}
</script>