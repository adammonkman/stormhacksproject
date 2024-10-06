<!-- src/Post.svelte -->
<script>
    import { createEventDispatcher } from 'svelte';
    import Button from "./lib/components/Button.svelte";

    export let post; // The post object, passed from Feed.svelte
    const dispatch = createEventDispatcher();
    let newComment = '';

    function submitComment() {
        if (newComment.trim()) {
            // Dispatch the comment to the parent (Feed.svelte)
            dispatch('addComment', newComment);
            newComment = ''; // Clear the input field after submitting
        }
    }
</script>

<!-- Post Content & Comment Input Form -->
<div id="posts">
    <p>{post.content}</p>

    <!-- Comment Input Section -->
    <div id="comment">
        <input id="text" type="text" placeholder="Add a comment..." 
        bind:value={newComment} on:keydown="{(e) => e.key === 'Enter' && submitComment()}" />
        <Button on:click={submitComment}> Comment </Button>
    </div>

    <!-- Display Comments Section -->
    {#if post.comments.length > 0}
        <div id="comment_section">
            <h4 id="comments">Comments:</h4>
            <ul id="ul">
                {#each post.comments as comment}
                    <li id="li">
                        {comment}
                    </li>
                {/each}
            </ul>
        </div>
    {/if}
</div>

<style>
    #li{
        padding: 0.5rem; 
        border-bottom: 1px solid white;
        font-size: 0.9rem;
    }
    #comments{
        margin-bottom: 0.5rem;
    }
    #posts{
        border: 1px solid black; 
        background-color: rgba(0, 0, 0, 0.626);
        color:white;
        margin-bottom: 1rem; 
        padding: 1rem; 
        border-radius: 8px;
        font-family: sans-serif;
    }

    #comment_section{
        margin-top: 1rem; 
    }
    #comment{
        margin-top: 1rem; 
        display: flex; 
        align-items: center;
    }
    #text{
        border-radius: 10px;
        flex: 1; 
        color:black;
        background-color: white;
        padding: 0.5rem;
        font-size: 1rem; 
        border: 3px solid white; 
        margin-right: 10px;
    }
    #ul{
        list-style: none; 
        padding-left: 0;
    }
</style>