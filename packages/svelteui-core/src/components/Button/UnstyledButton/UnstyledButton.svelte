<script lang="ts">
	import useStyles from './UnstyledButton.styles';
	import { Box } from '../../Box';
	import { useActions } from '$lib/internal';
	import type { UnstyledButtonProps as $$UnstyledButtonProps } from './UnstyledButton';

	interface $$Props extends $$UnstyledButtonProps {}

	export let use: $$Props['use'] = [],
		element: $$Props['element'] = undefined,
		className: $$Props['className'] = '',
		override: $$Props['override'] = {},
		root: $$Props['root'] = 'button';
	export { className as class };

	$: ({ cx, classes, getStyles } = useStyles(null, { name: 'UnstyledButton' }));
</script>

<Box
	bind:element
	use={[[useActions, use]]}
	class={cx(className, classes.root, getStyles({ css: override }))}
	{root}
	{...$$restProps}
>
	<slot />
</Box>
