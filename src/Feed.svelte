<!-- src/Feed.svelte -->
<script>
    import Post from './Post.svelte';
    export let addPoints;

    // Example hard-coded posts
    let posts = [
        { id: 1, content: 'Im sad', comments: [] },
        { id: 2, content: 'Need kind words rn plssss', comments: [] },
        { id: 3, content: 'Im going crazy!!!!', comments: [] },
        { id: 4, content: 'Had a bad day :(', comments: [] },
        { id: 5, content: 'My code dont freaking work!!!', comments: [] },
    ];

    function addComment(postId, comment) {
        // Find the post by ID and push the new comment to its comments array
        posts = posts.map(post => {
            if (post.id === postId) {
                return { ...post, comments: [...post.comments, comment] };
            }
            return post;
        });

        // Add points after a comment is added
        addPoints(1);
    }
</script>

<div>
    <!-- Pass each post to the Post component and handle the addComment event -->
    {#each posts as post}
        <Post {post} on:addComment={event => addComment(post.id, event.detail)} />
    {/each}
</div>
