<script lang="ts">
	import { writable } from 'svelte/store';
	import Time from './time.svelte';
	import Todo from './todo.svelte';
	import type { Work } from './work.type';

	let title = '';
	let todos = writable<Work[]>([]);
	let id = 0;

	function createTodo() {
		const todo: Work = {
			id,
			title
		};
		$todos.push(todo);
		$todos = $todos;
		title = '';

		id += 1;
	}
</script>

<div>
	<Time />

	<div class="input">
		<input
			type="text"
			bind:value={title}
			on:keydown={(e) => {
				e.key === 'Enter' && createTodo();
			}}
			placeholder="Todo List"
		/>
		<button on:click={createTodo}>+</button>
	</div>

	{#each $todos as todo}
		<Todo {todos} {todo} />
	{/each}
</div>

<style>
	@font-face {
		font-family: 'GmarketSansLight';
		src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansLight.woff')
			format('woff');
		font-weight: normal;
		font-style: normal;
	}
	:global(*) {
		font-family: GmarketSansLight;
	}
	:global(body > div) {
		width: 100%;
		max-width: 450px;
		height: 100%;
		margin: auto;
		background-color: #fff;
		max-height: 810px;
		box-shadow: 1px 4px 20px rgba(50, 50, 50, 0.1);
		border-radius: 1rem;
		position: relative;
	}

	:global(body) {
		background-color: #f4f4f4;
		padding: 0;
		display: flex;
		width: 100%;
		height: 100%;
		position: relative;
	}

	:global(html) {
		width: 100%;
		height: 100%;
		position: relative;
	}

	.input {
		margin: auto;
		margin-top: -1.5rem;
		width: calc(100% - 4rem);
		display: flex;
		justify-content: space-between;
		gap: 0.6rem;
	}
	.input input {
		width: 100%;
		padding: 0.7rem 1rem;
		border-radius: 2rem;
		outline: none;
		border: 1px solid rgba(0, 0, 0, 0.3);
	}
	.input button {
		width: 3rem;
		border-radius: 2rem;
		background-color: #ffc84d;
		border: #ffc84d;
		font-size: 1.4rem;
		color: white;
	}
</style>
