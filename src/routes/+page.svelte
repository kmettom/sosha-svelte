<script>
	import Counter from './Counter.svelte';
	import Campaigns from './Campaigns.svelte';
</script>

<svelte:head>
	<title>Dashboard</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		Dashboard
	</h1>

	<Counter />


	<div>
		My campaings
	</div>

	<Campaigns />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}


</style>
