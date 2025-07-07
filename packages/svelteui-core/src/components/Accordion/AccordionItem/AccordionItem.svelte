<script lang="ts">
	import { getContext } from 'svelte';
	import { Box } from '../../Box';
	import { UnstyledButton } from '../../Button';
	import { Collapse } from '../../Collapse';
	import type { AccordionContext } from '../Accordion';
	import { key } from '../key';
	import useStyles from './AccordionItem.styles';
	import type { AccordionItemProps as $$Props } from './AccordionItem';

	export let use: $$Props['use'] = [],
		element: $$Props['element'] = undefined,
		className: $$Props['className'] = '',
		override: $$Props['override'] = {},
		value: $$Props['value'] = undefined,
		chevronIcon: $$Props['chevronIcon'] = undefined,
		disabled: $$Props['disabled'] = false;
	export { className as class };

	const ctx: AccordionContext = getContext(key);

	function onClick() {
		$ctx.updateActive(value);
	}

	$: ({ cx, classes, getStyles } = useStyles(
		{
			radius: $ctx.radius,
			transitionDuration: $ctx.transitionDuration,
			chevronPosition: $ctx.chevronPosition,
			chevronSize: $ctx.chevronSize
		},
		{ name: 'AccordionItem' }
	));
</script>

<!--
@component

Item of an accordion.

@see https://svelteui.dev/core/accordion
@example
    ```svelte
    <Accordion.Item value="typescript">
      <div slot="control">Typescript Based</div>
      Content of the accordion item
    </Accordion.Item>
    ```

@slots
- chevronIcon: Custom chevron icon component
- control: Control content (required)
- default: Main content of the accordion item
-->

<Box
	class={cx(className, classes.root, getStyles({ css: override, variation: $ctx.variant }), {
		[classes.active]: $ctx.isItemActive(value)
	})}
	data-active={$ctx.isItemActive(value)}
	{use}
	{...$$restProps}
>
	<UnstyledButton
		class={classes.control}
		bind:element
		{disabled}
		id={$ctx.getRegionId(value)}
		aria-expanded={$ctx.isItemActive(value)}
		aria-controls={$ctx.getControlsId(value)}
		on:click={onClick}
		{use}
	>
		<span
			class={classes.chevron}
			data-rotate={!$ctx.disableChevronRotation && $ctx.isItemActive(value)}
		>
			<slot name="chevronIcon">
				<svelte:component this={chevronIcon || $ctx.chevron} />
			</slot>
		</span>
		<span class={classes.controlContent}>
			<slot name="control" {disabled} />
		</span>
	</UnstyledButton>
	<Collapse
		role="region"
		id={$ctx.getControlsId(value)}
		aria-labelledby={$ctx.getRegionId(value)}
		open={$ctx.isItemActive(value)}
		transitionDuration={$ctx.transitionDuration}
	>
		<div class={classes.panel}>
			<slot />
		</div>
	</Collapse>
</Box>
