<script lang="ts">
	import { get_current_component } from 'svelte/internal'
	import { El } from '../el'
	import { Label } from '../label'
	import type { SwitchProps } from './Switch.types'

	type $$Props = SwitchProps

	export let componentName: $$Props['componentName'] = 'switch'
	export let tag: $$Props['tag'] = 'input'
	export let id: $$Props['id'] = undefined
	export let color: $$Props['color'] = undefined
	export let disabled: $$Props['disabled'] = undefined
	export let description: $$Props['description'] = undefined
	export let inline: $$Props['inline'] = undefined
	export let name: $$Props['name'] = undefined
	export let label: $$Props['label'] = undefined
	export let value: $$Props['value'] = false
	export let reverse: $$Props['reverse'] = false
	export let checked: $$Props['checked'] = false
	export let role: $$Props['role'] = 'switch'
	export let type: $$Props['type'] = 'checkbox'
	export let _slots: Record<string, boolean> = $$slots

	const components = [
		{ component: get_current_component(), except: [] },
		...($$props.components ?? []),
	]

	function onChange(event: any) {
		checked = event.target.checked
		value = event.target.checked
	}

	let props: $$Props = {}
	let cssProps: $$Props = {}
	let _for: string | undefined = undefined
	$: {
		_for = id
		cssProps = {
			color,
		}

		props = {
			tag,
			checked,
			componentName,
			label,
			role,
			disabled,
			type,
			name,
		}
	}
</script>

<El componentName="{componentName}-wrapper" cssProps={{ inline, reverse }}>
	<El bind:id {...$$restProps} {cssProps} {...props} on:change={onChange} {components} />
	{#if label || _slots['default']}
		<Label for={_for} componentName="{componentName}-label">
			{#if _slots['default']}
				<slot />
			{:else}
				{label}
			{/if}
		</Label>
	{/if}
	{#if description || _slots['description']}
		<El componentName="{componentName}-description">
			{#if _slots['description']}
				<slot name="description" />
			{:else}
				{description}
			{/if}
		</El>
	{/if}
</El>
