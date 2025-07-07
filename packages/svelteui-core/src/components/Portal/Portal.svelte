<script lang="ts">
	import { useActions } from '$lib/internal';
	import { portal } from '@svelteuidev/composables';
	import type { PortalProps as $$Props } from './Portal';

	interface Props {
		use?: $$Props['use'];
		element?: $$Props['element'];
		class?: $$Props['className'];
		target?: $$Props['target'];
		position?: $$Props['position'];
		zIndex?: $$Props['zIndex'];
		children?: import('svelte').Snippet;
	}

	let {
		use = [],
		element = $bindable(undefined),
		class: className = '',
		target = 'body',
		position = 'relative',
		zIndex = 1,
		children
	}: Props = $props();
</script>

<div
	bind:this={element}
	use:useActions={use}
	use:portal={target}
	class={className}
	hidden
	style="position: {position}; zIndex: {zIndex};"
>
	{@render children?.()}
</div>
