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
<div style="border: 1px solid #ccc; margin-bottom: 1rem; padding: 1rem; border-radius: 8px;">
    <p>{post.content}</p>

    <!-- Comment Input Section -->
    <div style="margin-top: 1rem; display: flex; align-items: center;">
        <input 
            type="text" 
            placeholder="Add a comment..." 
            bind:value={newComment} 
            on:keydown="{(e) => e.key === 'Enter' && submitComment()}" 
            style="
                flex: 1; 
                padding: 0.5rem;
                font-size: 1rem; 
                border: 1px solid #ccc; 
                border-radius: 4px;
                margin-right: 10px;
                box-shadow: inset 0 1px 3px rgba(0,0,0,0.1);
            "
        />
        <Button on:click={submitComment}>
            Comment
        </Button>
    </div>

    <!-- Display Comments Section -->
    {#if post.comments.length > 0}
        <div style="margin-top: 1rem;">
            <h4 style="margin-bottom: 0.5rem;">Comments:</h4>
            <ul style="list-style: none; padding-left: 0;">
                {#each post.comments as comment}
                    <li style="
                        padding: 0.5rem; 
                        border-bottom: 1px solid #eee;
                        font-size: 0.9rem;
                    ">
                        {comment}
                    </li>
                {/each}
            </ul>
        </div>
    {/if}
</div>

<style>
    .button{
        background-color: #007bff; 
        color: white; 
        border: none; 
        padding: 0.5rem 1rem;
        border-radius: 4px; 
        cursor: pointer;
    }
</style>