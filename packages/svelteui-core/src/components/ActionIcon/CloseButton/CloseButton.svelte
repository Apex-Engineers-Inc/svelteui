<script lang="ts">
	import ActionIcon from '../ActionIcon.svelte';
	import CloseIcon from './CloseIcon.svelte';
	import { useActions } from '$lib/internal';
	import type { CloseButtonProps as $$Props } from './CloseButton';

	interface Props {
		use?: $$Props['use'];
		element?: $$Props['element'];
		class?: $$Props['className'];
		override?: $$Props['override'];
		iconSize?: $$Props['iconSize'];
		root?: $$Props['root'];
		color?: $$Props['color'];
		variant?: $$Props['variant'];
		size?: $$Props['size'];
		radius?: $$Props['radius'];
		loaderProps?: $$Props['loaderProps'];
		loading?: $$Props['loading'];
		disabled?: $$Props['disabled'];
		href?: $$Props['href'];
		external?: $$Props['external'];
		[key: string]: any;
	}

	let {
		use = [],
		element = $bindable(undefined),
		class: className = '',
		override = {},
		iconSize = 'md',
		root = 'button',
		color = 'gray',
		variant = 'hover',
		size = 'md',
		radius = 'sm',
		loaderProps = {
			size: 'xs',
			color: 'gray',
			variant: 'circle'
		},
		loading = false,
		disabled = false,
		href = '',
		external = false,
		...rest
	}: Props = $props();

	const iconSizes = {
		xs: 12,
		sm: 14,
		md: 16,
		lg: 20,
		xl: 24
	};
</script>

<!--
@component

CloseButton is a premade ActionIcon with close icon

@see https://svelteui.dev/core/action-icon
@example
    ```tsx
    <CloseButton /> // standard CloseButton
    ```
-->

<ActionIcon
	bind:element
	class={className}
	use={[[useActions, use]]}
	{override}
	{root}
	{color}
	{variant}
	{size}
	{radius}
	{loaderProps}
	{loading}
	{disabled}
	{href}
	{external}
	{...rest}
>
	<CloseIcon width={iconSizes[iconSize]} height={iconSizes[iconSize]} />
</ActionIcon>
