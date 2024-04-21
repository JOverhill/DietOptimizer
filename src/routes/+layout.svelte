<script>
	import Sidebar from './Sidebar.svelte';
	import './styles.css';
</script>

<div class="app">
	<Sidebar />
	<main>
		<slot />
		
	</main>
	
	<footer>
		<p>PLACEHOLDER -- visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn SvelteKit</p>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 10vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 0px;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 20px;
		margin-top: 10%;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
