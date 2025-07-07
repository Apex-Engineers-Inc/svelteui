<script lang="ts">
	import useStyles from './Burger.styles';
	import { UnstyledButton } from '../Button';
	import { colorScheme } from '$lib/styles';
	import { useActions } from '$lib/internal';
	import type { BurgerProps as $$BurgerProps } from './Burger';

	interface $$Props extends $$BurgerProps {}

	export let use: $$Props['use'] = [],
		element: $$Props['element'] = undefined,
		className: $$Props['className'] = '',
		override: $$Props['override'] = {},
		opened: $$Props['opened'] = true,
		color: $$Props['color'] = undefined,
		size: $$Props['size'] = 'md';
	export { className as class };

	$: _color = color ? color : $colorScheme === 'dark' ? 'white' : 'black';
	$: ({ classes, getStyles, cx } = useStyles({ color: _color, size, opened }, { name: 'Burger' }));
</script>

<UnstyledButton
	bind:element
	use={[[useActions, use]]}
	override={{ padding: 5 }}
	class={cx(className, classes.root, getStyles({ css: override }))}
	{...$$restProps}
>
	<span class={cx(classes.burger, { opened: opened })} />
</UnstyledButton>
