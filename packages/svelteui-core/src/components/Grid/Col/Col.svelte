<script lang="ts">
	import { getContext } from 'svelte';
	import { Box } from '../../Box';
	import type { GridContext } from '../Grid';
	import useStyles from './Col.styles';
	import type { ColProps as $$Props } from './Col';

	interface Props {
		use?: $$Props['use'];
		element?: $$Props['element'];
		class?: $$Props['className'];
		override?: $$Props['override'];
		span?: $$Props['span'];
		offset?: $$Props['offset'];
		offsetXs?: $$Props['offsetXs'];
		offsetSm?: $$Props['offsetSm'];
		offsetMd?: $$Props['offsetMd'];
		offsetLg?: $$Props['offsetLg'];
		offsetXl?: $$Props['offsetXl'];
		xs?: $$Props['xs'];
		sm?: $$Props['sm'];
		md?: $$Props['md'];
		lg?: $$Props['lg'];
		xl?: $$Props['xl'];
		children?: import('svelte').Snippet;
		[key: string]: any;
	}

	let {
		use = [],
		element = $bindable(undefined),
		class: className = '',
		override = {},
		span = undefined,
		offset = 0,
		offsetXs = 0,
		offsetSm = 0,
		offsetMd = 0,
		offsetLg = 0,
		offsetXl = 0,
		xs = undefined,
		sm = undefined,
		md = undefined,
		lg = undefined,
		xl = undefined,
		children,
		...rest
	}: Props = $props();

	// retrieves the reactive context so that Col has access
	// to the Grid cols, grow and spacing parameters
	const state: GridContext = getContext('Grid');
	let { cols, grow, spacing } = $derived($state);

	function isSpanValid(span: number) {
		return typeof span === 'number' && span > 0 && span % 1 === 0;
	}

	let _span = $derived(span || cols || 0);
	let valid = $derived(isSpanValid(_span) && _span <= cols);

	let { cx, classes, getStyles } = $derived(
		useStyles(
			{
				span: _span,
				cols,
				grow,
				spacing,
				offset,
				offsetXs,
				offsetSm,
				offsetMd,
				offsetLg,
				offsetXl,
				xs,
				sm,
				md,
				lg,
				xl
			},
			{ name: 'Col' }
		)
	);
</script>

{#if valid}
	<Box
		bind:element
		{use}
		class={cx(className, classes.root, getStyles({ css: override }))}
		{...rest}
	>
		{@render children?.()}
	</Box>
{/if}
