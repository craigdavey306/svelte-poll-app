<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	export let items: string[];
	export let activeItem: string;
</script>

<div class="tabs">
	<ul>
		{#each items as item}
			<li on:click={() => dispatch('tabChange', item)}>
				<div class:active={item === activeItem}>
					{item}
				</div>
			</li>
		{/each}
	</ul>
</div>

<style>
	.tabs {
		margin-bottom: 2.5rem;
	}

	ul {
		display: flex;
		justify-content: center;
		padding: 0;
		list-style-type: none;
	}

	li {
		margin: 0 1rem;
		font-size: 1.2rem;
		color: #555;
		cursor: pointer;
	}

	.active {
		--tab-active-color: #d91b42;
		color: var(--tab-active-color);
		border-bottom: 2px solid var(--tab-active-color);
		padding-bottom: 0.5rem;
	}
</style>
