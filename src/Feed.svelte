<!-- src/Feed.svelte -->
<script>
    import Post from './Post.svelte';
    export let addPoints;
    //import points from '/App.svelte'; //need points for animation can remove
  import App from './App.svelte';
    // Example hard-coded posts
    let posts = [
        { id: 1, content: 'Im sad', comments: [] },
        { id: 2, content: 'Need kind words rn plssss', comments: [] },
        { id: 3, content: 'Im going crazy!!!!', comments: [] },
        { id: 4, content: 'Had a bad day :(', comments: [] },
        { id: 5, content: 'My code dont freaking work!!!', comments: [] },
    ];
    let randomPoints = 0;
    function addComment(postId, comment) {
        // Find the post by ID and push the new comment to its comments array
        posts = posts.map(post => {
            if (post.id === postId) {
                flashPoint();
                return { ...post, comments: [...post.comments, comment] };
            }
            return post;
        });
         // Generate a random number between 1 and 10
         randomPoints = Math.floor(Math.random() * 20) + 1;

        // Add points after a comment is added
        
        addPoints(randomPoints);
    }

    function flashPoint() {
    const message = document.getElementById('+1');

    // Show the small message
    message.classList.remove('hidden');
    message.classList.add('visible');

    // Hide both elements after 3 seconds
    setTimeout(() => {
        message.classList.remove('visible');
        message.classList.add('hidden');
    }, 3000);  // 3 seconds
}
</script>
<h1 id="+1" class="hidden">+{randomPoints}</h1> <!--ANIMATION FOR POINT static-->
<div>
    
    <!-- Pass each post to the Post component and handle the addComment event -->
    {#each posts as post}
        <Post {post} on:addComment={event => addComment(post.id, event.detail)} />
    {/each}
</div>


