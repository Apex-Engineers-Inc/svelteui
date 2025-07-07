<script lang="ts">
	import { useActions } from '$lib/internal';
	import { portal } from '@svelteuidev/composables';
	import type { PortalProps as $$PortalProps } from './Portal';

	interface $$Props extends $$PortalProps {}

	export let use: $$Props['use'] = [],
		element: $$Props['element'] = undefined,
		className: $$Props['className'] = '',
		target: $$Props['target'] = 'body',
		position: $$Props['position'] = 'relative',
		zIndex: $$Props['zIndex'] = 1;
	export { className as class };
</script>

<div
	bind:this={element}
	use:useActions={use}
	use:portal={target}
	class={className}
	hidden
	style="position: {position}; zIndex: {zIndex};"
>
	<slot />
</div>
