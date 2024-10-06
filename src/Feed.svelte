<!-- src/Feed.svelte -->
<script>
    import Post from './Post.svelte';

    // Example hard-coded posts
    let posts = [
        { id: 1, content: 'Im sad', comments: [] },
        { id: 2, content: 'Need kind words rn plssss', comments: [] },
        { id: 3, content: 'Im going crazy!!!!', comments: [] }
    ];

    function addComment(postId, comment) {
        // Find the post by ID and push the new comment to its comments array
        posts = posts.map(post => {
            if (post.id === postId) {
                return { ...post, comments: [...post.comments, comment] };
            }
            return post;
        });
    }
</script>

<div>
    <!-- Pass each post to the Post component and handle the addComment event -->
    {#each posts as post}
        <Post {post} on:addComment={event => addComment(post.id, event.detail)} />
    {/each}
</div>
