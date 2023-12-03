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
    let addedPostIds = [];

    const addPostToCampaign = (post) => {
		newCampaign.posts = [...newCampaign.posts, post]
        addedPostIds = [...addedPostIds, post.id]
	}

    const addNewCampaign = () => {
		campaigns.update((value) => [...value, {id: campaignsCount + 1, name: newCampaign.name , posts: newCampaign.posts }])
        newCampaign.name = ''
		newCampaign.posts = []
        addedPostIds = []
	}

    onDestroy(unsubscribe)

</script>

<svelte:head>
	<title>Catalog</title>
	<meta name="description" content="Catalog"/>
</svelte:head>

<div class="text-column">
	<h1>Catalog</h1>
	<div class="active-campaigns">
		Number of active campaigns: {campaignsCount}
		{#if campaignsCount > 0}
			<div>
				<a class="btn" href="/">Check my active campaigns</a>
			</div>
		{/if}
	</div>

	<div>
		<input class="new-name-input" type="text" placeholder="Campaign name" bind:value={newCampaign.name}/>
		<button type="button" class="btn" on:click={() => {addNewCampaign()}}>Save new campaign</button>
	</div>
	<div class="added-posts">
		Added posts: {addedPostIds}
		{#if addedPostIds.length === 0} No posts added yet{/if}
	</div>
	<div class="posts-wrapper">
		{#each posts as post}
			<button class="post" class:added={addedPostIds.includes(post.id)} on:click={() => {addPostToCampaign(post)}}>
				<div class="post-title">
					<h2>{post.title}</h2>
				</div>
				<div class="post-content">
					<p>{post.content}</p>
				</div>
			</button>
		{/each}
	</div>

</div>

<style>
	.active-campaigns{
		margin-bottom: 20px;

	}
	.new-name-input{
		padding: 10px;
		border-radius: 10px;
	}
	.added-posts{
		margin-top: 20px;
	}
	.posts-wrapper{
		margin-top: 20px;
	}
	.post{
		display: inline-block;
		border: 2px solid var(--gray);
		border-radius: 10px;
		width: 200px;
		margin: 10px;
		padding: 10px;
		text-align: center;
		cursor: pointer;
	}
	.post.added,
	.post:hover{
		border: 2px solid var(--yellow);
	}

</style>
