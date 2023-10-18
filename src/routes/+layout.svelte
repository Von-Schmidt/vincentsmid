<script>
	import './styles.css';
	import Background from "./Background.svelte";

</script>

<div class="app">
	<main>
		<slot />
	</main>
	<Background />
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}

</style>