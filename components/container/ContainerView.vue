<template>
  <div class="container-view grid [&>*:not(.container-item)]:col-[contained]">
	  <template v-for="([variant, label]) in Object.entries(VARIANTS)" :key="variant">
		  <h2 class="text-3xl mt-16 mb-4 py-4 text-center border-y-2 border-dashed border-black">
			  {{ label }}
			  <br />
			  <small class="text-gray-500 text-sm">variant="{{ variant }}"</small>
		  </h2>

		  <!-- LayoutItem with any child element -->
		  <ContainerItem :variant="variant as any">
			  <!-- Placeholder content -->
			  <img src="https://picsum.photos/2600/500" alt="Image" />
			  <p class="pt-3">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eros nunc, luctus id finibus eu, rhoncus vel diam. Fusce nec mi non neque accumsan sollicitudin. Vivamus ac vehicula nunc. Duis vehicula vulputate vulputate. Donec nec tempor metus. Sed consequat libero nec leo fermentum, ac tempor mauris semper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Donec consequat, arcu in iaculis gravida, lectus mi faucibus neque, id malesuada lacus eros eget sem. Integer facilisis bibendum dolor eget ornare. Suspendisse potenti.</p>
			  <p class="py-3">ALorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eros nunc, luctus id finibus eu, rhoncus vel diam. Fusce nec mi non neque accumsan sollicitudin. Vivamus ac vehicula nunc. Duis vehicula vulputate vulputate. Donec nec tempor metus. Sed consequat libero nec leo fermentum, ac tempor mauris semper. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Donec consequat, arcu in iaculis gravida, lectus mi faucibus neque, id malesuada lacus eros eget sem. Integer facilisis bibendum dolor eget ornare. Suspendisse potenti.</p>
		  </ContainerItem>

		  <!-- LayoutItem with columns -->
		  <ContainerItem :variant="variant as any">
			  <ContainerCols :cols="2">
				  <!-- Placeholder content -->
				  <!-- Supports background colors on each column -->
				  <div class="bg-orange-200 text-center font-bold py-6">1</div>
				  <div class="bg-violet-300 text-center font-bold py-6">2</div>
				  <div class="bg-orange-300 text-center font-bold py-6">3</div>
				  <div class="bg-violet-400 text-center font-bold py-6">4</div>
			  </ContainerCols>
		  </ContainerItem>

		  <ContainerItem class="mt-2" :variant="variant as any">
			  <ContainerCols :cols="3">
				  <!-- Placeholder content -->
				  <!-- Supports background colors on each column -->
				  <div class="bg-orange-200 text-center font-bold py-6">1</div>
				  <div class="bg-blue-300 text-center font-bold py-6">2</div>
				  <div class="bg-violet-300 text-center font-bold py-6">3</div>
				  <div class="bg-orange-300 text-center font-bold py-6">4</div>
				  <div class="bg-blue-400 text-center font-bold py-6">5</div>
				  <div class="bg-violet-400 text-center font-bold py-6">6</div>
			  </ContainerCols>
		  </ContainerItem>

		  <ContainerItem class="mt-2" :variant="variant as any">
			  <ContainerCols :cols="4">
				  <!-- Placeholder content -->
				  <!-- Supports background colors on each column -->
				  <div class="bg-orange-200 text-center font-bold py-6">1</div>
				  <div class="bg-green-300 text-center font-bold py-6">2</div>
				  <div class="bg-blue-300 text-center font-bold py-6">3</div>
				  <div class="bg-violet-300 text-center font-bold py-6">4</div>
				  <div class="bg-orange-300 text-center font-bold py-6">5</div>
				  <div class="bg-green-400 text-center font-bold py-6">6</div>
				  <div class="bg-blue-400 text-center font-bold py-6">7</div>
				  <div class="bg-violet-400 text-center font-bold py-6">8</div>
			  </ContainerCols>
		  </ContainerItem>
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
.container-view {
	grid-template-columns:
		[full-start] var(--full-width)
		[breakout-start] var(--breakout-width)
		[contained-start] var(--contained-width) [contained-end]
		var(--breakout-width) [breakout-end]
		var(--full-width) [full-end];
}
</style>

<script setup lang="ts">
import ContainerCols from "@/views/ContainerCols.vue";
import ContainerItem from "@/views/ContainerItem.vue";

const VARIANTS = {
	contained: 'Contained (default)',
	breakout: 'Breakout',
	'breakout-l': 'Breakout left',
	'breakout-r': 'Breakout right',
	full: 'Full width',
	'full-contained': 'Full width contained',
}
</script>