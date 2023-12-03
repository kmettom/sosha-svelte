<script>
	import Campaigns from './Campaigns.svelte';
</script>

<svelte:head>
	<title>Dashboard</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		My campaigns
	</h1>
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
	h2 {
		font-weight: 600;
	}


</style>
