<script>
	import TodoList from './components/TodoList.svelte';
</script>

<main>
	<h1 class="title">todopslevel</h1>
	<TodoList />
</main>

<style type="text/scss">
	@charset "utf-8";
	@import 'bulma/bulma';

	main {
		font-family: BlinkMacSystemFont, -apple-system, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	.title {
		color: chocolate;
		text-transform: uppercase;
		font-weight: 100;
	}
</style>