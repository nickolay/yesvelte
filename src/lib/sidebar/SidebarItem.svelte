<script lang="ts">
	import { get_current_component } from 'svelte/internal'
	import { Icon } from '../icon'
	import { El, type ElProps } from '../el'
	import type { SidebarItemProps } from './Sidebar.types'
	import { Popup } from '../popup'

	type $$Props = SidebarItemProps

	export let componentName: $$Props['componentName'] = 'sidebar-item'
	export let disabled: $$Props['disabled'] = undefined
	export let active: $$Props['active'] = undefined
	export let icon: $$Props['icon'] = undefined
	export let title: $$Props['title'] = undefined
	export let href: $$Props['href'] = undefined

	const components = [
		{ component: get_current_component(), except: [] },
		...($$props.components ?? []),
	]

	let wrapperProps: Partial<ElProps>
	$: wrapperProps = {
		tag: 'li',
		componentName: componentName + '-wrapper',
	}

	let props: Partial<ElProps>
	$: props = {
		tag: href ? 'a' : 'div',
		href,
		componentName,
	}

	$: dropdown = $$slots['default']
	$: cssProps = {
		disabled,
		dropdown,
		active,
	}
</script>

<El {components} {...$$restProps} {...wrapperProps} cssProps={{ dropdown }}>
	<El on:click {...props} {cssProps}>
		{#if icon || $$slots['start']}
			<El tag="span" componentName="{componentName}-icon">
				<slot name="start">
					<Icon name={icon} />
				</slot>
			</El>
		{/if}
		{#if title || $$slots['title']}
			<El tag="span" componentName="{componentName}-title">
				<slot name="title">
					{title}
				</slot>
			</El>
		{/if}
		{#if $$slots['end']}
			<El componentName="{componentName}-end">
				<slot name="end" />
			</El>
		{/if}
	</El>

	{#if $$slots['default']}
		<Popup
			tag="ul"
			trigger="click"
			bind:show={active}
			autoClose={false}
			placement="right-start"
			componentName="{componentName}-menu">
			<slot />
		</Popup>
	{/if}
</El>
