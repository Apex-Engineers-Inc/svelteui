<script lang="ts">
	import useStyles from './UnstyledButton.styles';
	import { Box } from '../../Box';
	import { useActions } from '$lib/internal';
	import type { UnstyledButtonProps as $$Props } from './UnstyledButton';

	interface Props {
		use?: $$Props['use'];
		element?: $$Props['element'];
		class?: $$Props['className'];
		override?: $$Props['override'];
		root?: $$Props['root'];
		children?: import('svelte').Snippet;
		[key: string]: any;
	}

	let {
		use = [],
		element = $bindable(undefined),
		class: className = '',
		override = {},
		root = 'button',
		children,
		...rest
	}: Props = $props();

	let { cx, classes, getStyles } = $derived(useStyles(null, { name: 'UnstyledButton' }));
</script>

<Box
	bind:element
	use={[[useActions, use]]}
	class={cx(className, classes.root, getStyles({ css: override }))}
	{root}
	{...rest}
>
	{@render children?.()}
</Box>
