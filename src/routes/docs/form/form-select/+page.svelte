<script>
	import { Page, Preview, Doc } from '$components'
	import FormSelectDefault from './FormSelectDefault.svelte'
	import FormSelectColumn from './FormSelectColumn.svelte'
	import FormSelectState from './FormSelectState.svelte'
	import FormSelectHint from './FormSelectHint.svelte'
	import FormSelectItemsBind from './FormSelectItemsBind.svelte'
	import FormSelectKey from './FormSelectKey.svelte'
	import FormSelectEvents from './FormSelectEvents.svelte'
	import FormSelectObject from './FormSelectObject.svelte'
	import FormSelectDynamicItems from './FormSelectDynamicItems.svelte'
	import FormSelectRequired from './FormSelectRequired.svelte'
	import FormSelectMultiple from './FormSelectMultiple.svelte'
	import FormSelectSlots from './FormSelectSlots.svelte'
</script>

<Page title="FormSelect">
	<p slot="description">
		<code>FormSelect</code> component supports all props and events of
		<a href="/docs/select">Select</a>
		and also have some additional features like <code>label</code>, <code>hint</code>,
		<code>required</code>,
		<code>cols</code>, etc. to make it easy to use in a form.
	</p>

	<Doc title="Label">
		<Preview src="./FormSelectDefault.svelte">
			<FormSelectDefault />
		</Preview>
	</Doc>

	<Doc title="Key">
		<Preview src="./FormSelectKey.svelte">
			<FormSelectKey />
		</Preview>
	</Doc>

	<Doc title="Hint/Validation Message">
		<Preview src="./FormSelectHint.svelte">
			<FormSelectHint />
		</Preview>
	</Doc>

	<Doc title="Events">
		<Preview src="./FormSelectEvents.svelte">
			<FormSelectEvents />
		</Preview>
	</Doc>

	<Doc title="Bind as Object">
		<Preview src="./FormSelectObject.svelte">
			<FormSelectObject />
		</Preview>
	</Doc>

	<Doc title="State">
		<Preview src="./FormSelectState.svelte">
			<FormSelectState />
		</Preview>
	</Doc>

	<Doc title="Required">
		<Preview src="./FormSelectRequired.svelte">
			<FormSelectRequired />
		</Preview>
	</Doc>

	<Doc title="Multiple">
		<Preview src="./FormSelectMultiple.svelte">
			<FormSelectMultiple />
		</Preview>
	</Doc>

	<!-- <Doc title="Slots">
		<Preview src="./FormSelectSlots.svelte">
			<FormSelectSlots />
		</Preview>
	</Doc> -->

	<Doc title="Dynamic Items">
		<Preview src="./FormSelectDynamicItems.svelte">
			<FormSelectDynamicItems />
		</Preview>
	</Doc>

	<Doc title="Bind Item">
		<Preview src="./FormSelectItemsBind.svelte">
			<FormSelectItemsBind />
		</Preview>
	</Doc>

	<Doc title="Layout">
		<Preview src="./FormSelectColumn.svelte">
			<FormSelectColumn />
		</Preview>
	</Doc>
</Page>
