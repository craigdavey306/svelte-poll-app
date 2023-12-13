<script lang="ts">
	import PollStore from '../../stores/PollStore';
	import PollDetails from './PollDetails.svelte';
</script>

<div class="poll-list">
	{#each $PollStore as poll (poll.id)}
		<PollDetails {poll} on:vote />
	{/each}
</div>

<style>
	.poll-list {
		display: grid;
		grid-template-columns: 1fr 1fr;
	}
</style>
