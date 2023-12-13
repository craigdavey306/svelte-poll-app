<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { Button } from '$lib';
	import PollStore from '../../stores/PollStore';

	let dispatch = createEventDispatcher();

	let fields = { question: '', answerA: '', answerB: '' };
	let errors = { question: '', answerA: '', answerB: '' };
	let valid = false;

	const handleOnSubmit = () => {
		valid = true;

		if (fields.question.trim().length < 5) {
			valid = false;
			errors.question = 'Question must be at least 5 characters long.';
		} else {
			errors.question = '';
		}

		if (fields.answerA.trim().length < 1) {
			valid = false;
			errors.answerA = 'Answer A must have a value.';
		} else {
			errors.answerA = '';
		}

		if (fields.answerB.trim().length < 1) {
			valid = false;
			errors.answerB = 'Answer B must have a value.';
		} else {
			errors.answerB = '';
		}

		// add new poll
		if (valid) {
			const poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
			PollStore.update((currentPolls) => {
				return [poll, ...currentPolls];
			});
			dispatch('add');
		}
	};
</script>

<form on:submit|preventDefault={handleOnSubmit}>
	<div class="form-field">
		<label for="question">Poll Question</label>
		<input type="text" name="question" id="question" bind:value={fields.question} />
		<div class="error">{errors.question}</div>
	</div>
	<div class="form-field">
		<label for="answer-a">Answer A</label>
		<input type="text" name="answer-a" id="answer-a" bind:value={fields.answerA} />
		<div class="error">{errors.answerA}</div>
	</div>
	<div class="form-field">
		<label for="answer-b">Answer B</label>
		<input type="text" name="answer-b" id="answer-b" bind:value={fields.answerB} />
		<div class="error">{errors.answerB}</div>
	</div>
	<Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
	form {
		width: 400px;
		margin: 0 auto;
		text-align: center;
	}

	.form-field {
		margin: 1.2rem auto;
	}

	input {
		width: 100%;
		border-radius: 6px;
	}

	label {
		margin: 0.625rem auto;
		text-align: left;
	}

	.error {
		font-weight: bold;
		font-size: 12px;
		color: #d91b42;
	}
</style>
