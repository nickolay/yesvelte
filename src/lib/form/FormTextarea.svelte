<script lang="ts">
	import FormField from './FormField.svelte'
	import { Textarea } from '../textarea'
	import type { FormTextAreaProps } from './Form.types'

	import { get_current_component } from 'svelte/internal'
	import { El } from '../el'

	type $$Props = FormTextAreaProps

	export let componentName: $$Props['componentName'] = 'form-textarea'
	export let tag: $$Props['tag'] = 'textarea'
	export let disabled: $$Props['disabled'] = undefined
	export let borderRounded: $$Props['borderRounded'] = undefined
	export let borderFlush: $$Props['borderFlush'] = undefined
	export let placeholder: $$Props['placeholder'] = undefined
	export let readonly: $$Props['readonly'] = undefined
	export let required: $$Props['required'] = undefined
	export let rows: $$Props['rows'] = 3
	export let name: $$Props['name'] = undefined
	export let size: $$Props['size'] = undefined
	export let state: $$Props['state'] = undefined
	export let type: $$Props['type'] = undefined
	export let value: $$Props['value'] = undefined
	export let label: $$Props['label'] = undefined
	export let hint: $$Props['hint'] = undefined
	export let minlength: $$Props['minlength'] = undefined
	export let maxlength: $$Props['maxlength'] = undefined
	export let cols: $$Props['cols'] = undefined

	const components = [
		{ component: get_current_component(), except: [] },
		...($$props.components ?? []),
	]
	let id: string
	let props: $$Props = {}
	let teaxtareaProps: $$Props = {}

	$: {
		props = {
			required,
			label,
			hint,
			state,
			componentName,
		}

		teaxtareaProps = {
			tag,
			placeholder,
			disabled,
			readonly,
			type,
			required,
			size,
			state,
			borderRounded,
			borderFlush,
			rows,
			name,
			minlength,
			maxlength,
			cols,
		}
	}
</script>

<FormField {id} {...props} {...$$restProps}>
	<slot name="label" slot="label" />
	<svelte:fragment slot="group">
		<slot name="start">
			{#if $$slots['start-icon']}
				<El componentName="{componentName}-icon">
					<slot name="start-icon" />
				</El>
			{/if}
		</slot>
		<Textarea bind:id {components} {...teaxtareaProps} bind:value />
		<slot name="end">
			{#if $$slots['end-icon']}
				<El componentName="{componentName}-icon">
					<slot name="end-icon" />
				</El>
			{/if}
		</slot>
	</svelte:fragment>
	<slot name="hint" slot="hint" />
</FormField>
