<!-- src/Feed.svelte -->
<script>
    import Post from './Post.svelte';

    // Example hard-coded posts
    let posts = [
        { id: 1, content: 'This is the first post!', comments: [] },
        { id: 2, content: 'Here is another interesting post.', comments: [] },
        { id: 3, content: 'I love sharing thoughts with everyone!', comments: [] }
    ];

    function addComment(postId, comment) {
        // Find the post and add the comment
        const post = posts.find(p => p.id === postId);
        if (post) {
            post.comments.push(comment);
        }
    }
</script>

<div>
    {#each posts as post}
        <Post {post} on:addComment={event => addComment(post.id, event.detail)} />
    {/each}
</div>
