<script lang="ts">
	import { get_current_component } from 'svelte/internal'
	import { El } from '../el'
	import type { CheckboxGroupProps } from './Checkbox.types'
	import Checkbox from './Checkbox.svelte'

	type $$Props = CheckboxGroupProps

	interface $$Slots {
		default: { index?: number; item?: any }
	}

	export let color: $$Props['color'] = undefined
	export let componentName: $$Props['componentName'] = 'checkbox-group'
	export let inline: $$Props['inline'] = undefined
	export let items: $$Props['items'] = undefined
	export let name: $$Props['name'] = undefined
	export let reverse: $$Props['reverse'] = undefined
	export let value: $$Props['value'] = undefined
	export let key: $$Props['key'] = undefined

	const components = [
		{ component: get_current_component(), except: [] },
		...($$props.components ?? []),
	]

	let element: HTMLElement
	let props: $$Props = {}

	$: props = {
		inline,
		name: name ?? element?.id,
		color,
		reverse,
	}

	$: getKey = (item: any) => {
		if (key) {
			return typeof key === 'string' ? item[key] : key(item)
		} else {
			return item
		}
	}

	function onChange(event: any) {
		if (value === undefined) value = []

		if (items != undefined && items?.length > 0) {
			const selectedValue = event.target?.value
			const selectedChecked = event.target?.checked

			if (selectedChecked) {
				value.push(selectedValue)
			} else {
				var _index = value.indexOf(selectedValue)
				if (_index !== -1) {
					value.splice(_index, 1)
				}
			}
			value = value
		}
	}
</script>

<El {components} {componentName} bind:element {...$$restProps}>
	{#if items}
		{#each items as item, index (index)}
			<Checkbox
				{...props}
				value={getKey(item)}
				checked={value?.includes(getKey(item))}
				on:change={onChange}>
				<slot {index} {item}>{item}</slot>
			</Checkbox>
		{/each}
	{:else}
		<slot />
	{/if}
</El>
