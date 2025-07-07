<script lang="ts">
	import { useActions } from '$lib/internal';
	import { randomID } from '$lib/styles';
	import useStyles from './Switch.styles';
	import type { SwitchProps as $$Props } from './Switch';

	interface Props {
		use?: $$Props['use'];
		element?: $$Props['element'];
		class?: $$Props['className'];
		override?: $$Props['override'];
		color?: $$Props['color'];
		size?: $$Props['size'];
		radius?: $$Props['radius'];
		insideLabelSize?: $$Props['insideLabelSize'];
		transitionFunction?: $$Props['transitionFunction'];
		id?: $$Props['id'];
		label?: $$Props['label'];
		onLabel?: $$Props['onLabel'];
		offLabel?: $$Props['offLabel'];
		disabled?: $$Props['disabled'];
		checked?: $$Props['checked'];
	}

	let {
		use = [],
		element = $bindable(undefined),
		class: className = '',
		override = {},
		color = 'blue',
		size = 'sm',
		radius = 'xl',
		insideLabelSize = undefined,
		transitionFunction = 'linear',
		id = randomID(),
		label = '',
		onLabel = '',
		offLabel = '',
		disabled = false,
		checked = $bindable(false)
	}: Props = $props();

	let { cx, classes, getStyles } = $derived(
		useStyles(
			{
				color,
				offLabel,
				onLabel,
				insideLabelSize,
				radius,
				size,
				transitionFunction
			},
			{ name: 'Switch' }
		)
	);
</script>

<!--
@component

A user can use this component to enable/disable something, normally used for boolean values or for binary actions.

@see https://svelteui.dev/core/switch
@example
    ```tsx
    <Switch/> // standard switch
    <Switch label="Lights" onLabel="ON" offLabel="OFF"/> // switch with labels
    ```
-->
<div class={cx(className, classes.root)}>
	<input
		bind:this={element}
		{id}
		{disabled}
		use:useActions={use}
		bind:checked
		type="checkbox"
		class={cx(className, classes.input, getStyles({ css: override }))}
		class:disabled
	/>
	{#if label}
		<label for={id} class={classes.label}>
			{label}
		</label>
	{/if}
</div>

<style>
	.switch {
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.label {
		padding-left: 10px;
	}
</style>
