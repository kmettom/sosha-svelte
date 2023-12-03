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
        console.log("campaignsData" , campaignsData)
        // campaignsData = campaigns
	})

    onDestroy(() => {
        unsubscribe()
    })

</script>

<div class="campaigns">
	<div>
		<h2>Campaigns</h2>
		<div class="campaigns-wrapper">
			{#if campaignsData.length > 0}
				{#each campaignsData as campaign}
					<div class="campaign">
						<div class="campaign-name">
							{campaign.name}
						</div>
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
			{/if}
		</div>
	</div>
</div>

<style>
    .campaigns-wrapper {
        display: flex;
        max-width: 800px;
        margin: 0 auto;
    }

</style>
