<script>
	import './styles.css';
	import Auth from './Auth.svelte';
</script>

<div class="app">
	<main>
		<Auth />
		<slot />
	</main>
</div>

<style>
	main {
		/* padding-top: 4rem; */
	}
</style>
