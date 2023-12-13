<script lang="ts">
	import { fade } from 'svelte/transition';
	import { flip } from 'svelte/animate';
	import PollStore from '../../stores/PollStore';
	import PollDetails from './PollDetails.svelte';
</script>

<div class="poll-list">
	{#each $PollStore as poll (poll.id)}
		<div transition:fade animate:flip={{ duration: 500 }}>
			<PollDetails {poll} />
		</div>
	{/each}
</div>

<style>
	.poll-list {
		display: grid;
		grid-template-columns: 1fr 1fr;
	}
</style>
