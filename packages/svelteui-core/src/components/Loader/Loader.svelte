<script lang="ts">
	import { useActions } from '$lib/internal';
	import Circle from './loaders/Circle.svelte';
	import Bars from './loaders/Bars.svelte';
	import Dots from './loaders/Dots.svelte';
	import { LOADER_SIZES, getCorrectShade } from './Loader.styles';
	import type { LoaderProps as $$LoaderProps } from './Loader';

	interface $$Props extends $$LoaderProps {}

	export let use: $$Props['use'] = [],
		element: $$Props['element'] = undefined,
		className: $$Props['className'] = '',
		size: $$Props['size'] = 'md',
		color: $$Props['color'] = 'blue',
		variant: $$Props['variant'] = 'circle';
	export { className as class };

	/** Loader logic */
	const LOADERS = {
		bars: Bars,
		circle: Circle,
		dots: Dots
	};

	const defaultLoader = variant in LOADERS ? variant : 'circle';
</script>

<!--
@component
The Loader component creates a loading icon. There are three different Loaders with the circle as the default.

@see https://svelteui.dev/core/loader
@example
    ```tsx
    <Loader color='green' size='lg' variant='bars' />
    ```
-->
<svelte:component
	this={LOADERS[defaultLoader]}
	bind:this={element}
	use={[[useActions, use]]}
	color={color === 'white' ? 'white' : getCorrectShade(color)}
	size={LOADER_SIZES[size] || size}
	class={className}
	{...$$restProps}
/>
