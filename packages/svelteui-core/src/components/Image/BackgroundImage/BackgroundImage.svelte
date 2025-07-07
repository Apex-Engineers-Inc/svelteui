<script lang="ts">
	import useStyles from './BackgroundImage.styles';
	import { useActions } from '$lib/internal';
	import type { BackgroundImageProps as $$Props } from './BackgroundImage';

	interface Props {
		use?: $$Props['use'];
		element?: $$Props['element'];
		class?: $$Props['className'];
		override?: $$Props['override'];
		radius?: $$Props['radius'];
		src?: $$Props['src'];
		width?: $$Props['width'];
		height?: $$Props['height'];
		children?: import('svelte').Snippet;
	}

	let {
		use = [],
		element = $bindable(undefined),
		class: className = '',
		override = {},
		radius = 0,
		src = '',
		width = undefined,
		height = undefined,
		children
	}: Props = $props();

	let { cx, classes, getStyles } = $derived(
		useStyles({ height, radius, src, width }, { name: 'BackgroundImage' })
	);
</script>

<!--
@component

BackgroundImage component can be used to add any content on image. It is useful for hero headers and other similar sections

@see https://svelteui.dev/core/image
@example
    ```svelte
		<script>
			const src = 'https://images.unsplash.com/photo-1649014048485-590f93c42936?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80'
		</script>

		<BackgroundImage radius="sm" {src}>
			This content will be shown over the image
		</BackgroundImage>
    ```

	It is suggested to wrap your component in a container element
-->

<div
	bind:this={element}
	use:useActions={use}
	class={cx(className, classes.root, getStyles({ css: override }))}
>
	{#if children}{@render children()}{:else}Text{/if}
</div>
