<script>
    import {campaigns} from '../stores.js'
    import {get} from 'svelte/store'
    import {onDestroy, onMount} from 'svelte'

    let campaignsCount = 0
    let campaignsData = []

    const unsubscribe = campaigns.subscribe((value) => {
        campaignsCount = value.length
        campaignsData = value
    })

    onMount(() => {
        campaignsData = get(campaigns)
        console.log("campaignsData", campaignsData)
    })

    onDestroy(() => {
        unsubscribe()
    })

</script>

<div class="campaigns">
	{#if campaignsData.length == 0}
		<p class="no-campaigns">
			<strong>No campaigns added yet</strong>
		</p>
	{/if}
	<div class="campaigns-wrapper">
		{#each campaignsData as campaign}
			<div class="campaign">
				<div class="campaign-name">
					<strong>Name:</strong> {campaign.name}
				</div>
				<div><strong>Posts:</strong></div>
				<div class="campaign-posts">
					<ol>
						{#each campaign.posts as post}
							<li>
								{post.title}
							</li>
						{/each}
					</ol>
				</div>
			</div>
		{/each}
	</div>
	<div class="btn-wrapper">
		<a class="btn" href="/catalog" >Add campaign</a>
	</div>
</div>

<style>
    .campaigns-wrapper {
        max-width: 800px;
        margin: 0 auto;
    }
	.no-campaigns{
		text-align: center;
	}
	.campaign{
		vertical-align: top;
		display: inline-block;
		width: 300px;
		margin: 10px;
		padding: 10px;
		border-radius: 10px;
		border: 2px solid var(--gray);
	}
	.btn-wrapper{
		text-align: center;
		margin-top: 10px;
	}

</style>
