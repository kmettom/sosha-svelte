<script>
 	import { posts } from './posts.js';

    import { campaigns } from '../../stores.js'
    import { onDestroy } from 'svelte'

    let campaignsCount = 0

    const unsubscribe = campaigns.subscribe((value) => campaignsCount = value.length)

	let newCampaign = {
        name: '',
		posts: [],
	}

    const addPostToCampaign = (post) => {
		newCampaign.posts = [...newCampaign.posts, post]
        console.log("newCampaign" , newCampaign)
	}

    const addNewCampaign = () => {
		campaigns.update((value) => [...value, {id: campaignsCount + 1, name: newCampaign.name , posts: newCampaign.posts }])
        newCampaign.name = ''
		newCampaign.posts = []
	}

    campaigns.subscribe((value) => {
        console.log("campaigns" , value)
    })

    onDestroy(unsubscribe)

</script>

<svelte:head>
	<title>Catalog</title>
	<meta name="description" content="Catalog"/>
</svelte:head>

<div class="text-column">
	<h1>Catalog</h1>
	<div>
		Number of active campaigns: {campaignsCount}
		{#if campaignsCount > 0}
			<div>
				<a class="btn btn-primary" href="/">Check my active campaigns</a>
			</div>
		{/if}
	</div>

	<p>Pick posts to for your new campaign and save your new campaign</p>
	<div>
		<input type="text" placeholder="Campaign name" bind:value={newCampaign.name}/>
		<button type="button" class="btn btn-primary" on:click={() => {addNewCampaign()}}>Save new campaign</button>
	</div>
	<div class="posts-wrapper">
		{#each posts as post}
			<div class="post"  on:click={() => {addPostToCampaign(post)}}>
				<div class="post-title">
					<h2>{post.title}</h2>
				</div>
				<div class="post-content">
					<p>{post.content}</p>
				</div>
			</div>
		{/each}
	</div>

</div>

<style>
	.posts-wrapper{

	}
	.post{
		display: inline-block;
		border: 2px solid var(--gray);
		border-radius: 10px;
		/*width: 300px;*/
		margin: 10px;
		padding: 10px;
		text-align: center;
		cursor: pointer;
	}
	.post:hover{
		border: 2px solid var(--yellow);
	}
</style>
