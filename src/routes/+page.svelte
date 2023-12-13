<script lang="ts">
	import { Header, Footer, Tabs, CreatePollForm, PollList } from '$lib';
	import type { Poll } from '$lib/types';
	import type { ComponentEvents } from 'svelte';

	type Tab = 'Current Polls' | 'Add New Poll';

	let items: Tab[] = ['Current Polls', 'Add New Poll'];
	let activeItem = items[0];

	const handleTabChange = (e: ComponentEvents<Tabs>['tabChange']) => {
		activeItem = e.detail;
	};

	const handleAdd = (e: ComponentEvents<PollList>['add']) => {
		activeItem = 'Current Polls';
	};
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={handleTabChange} />
	{#if activeItem === 'Current Polls'}
		<PollList />
	{:else if activeItem === 'Add New Poll'}
		<CreatePollForm on:add={handleAdd} />
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>
