<script lang="ts">
	import type { Writable } from 'svelte/store';
	import type { Work } from './work.type';

	export let todos: Writable<Work[]>;
	export let todo: Work;

	let isEdit = false;
	let temp = '';

	function onEdit() {
		isEdit = true;
		temp = todo.title;
	}

	function offEdit() {
		isEdit = false;
	}

	function updateOne() {
		todo.title = temp;
		offEdit();
	}

	function deleteOne() {
		$todos = $todos.filter((t) => t.id !== todo.id);
	}
</script>

<div class="list">
	{#if isEdit}
		<div>
			<input
				bind:value={temp}
				on:keydown={(e) => {
					e.key === 'Enter' && updateOne();
				}}
			/>
			<button on:click={updateOne}>Ok</button>
			<button on:click={offEdit}>Cancel</button>
		</div>
	{:else}
		<div>
			<label>
				<input type="checkbox" for="" />
				<span>
					{todo.title}
				</span>
			</label>
			<button on:click={onEdit}>Edit</button>
			<button on:click={deleteOne}>Delete</button>
		</div>
	{/if}
</div>

<style>
	.list {
		padding: 0.5rem 2rem;
		margin-top: 1rem;
	}
	.list > div {
		position: relative;
		display: flex;
		align-items: center;
	}
	.list > div::before {
		position: absolute;
		display: inline-block;
		width: 0.2rem;
		height: 100%;
		content: '';
		margin-right: 1rem;
		background-color: #6393da;
	}
	.list > div > label {
		padding-left: 1rem;
		width: 100%;
	}
	input:checked + span {
		text-decoration: line-through;
		color: gray;
		opacity: 0.5;
	}
	.list > div > label input:checked + span:hover {
		opacity: 1;
	}
	input[type='checkbox'] {
		display: none;
	}
	button {
		margin: 0;
		color: #bcbcbc;
		border: none;
	}
	div > button:last-child {
		color: #fff;
		background-color: #ff5b5b;
	}
</style>
