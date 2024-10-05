<!-- src/Post.svelte -->
<script>
    import { createEventDispatcher } from 'svelte';

    export let post;
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

<div style="border: 1px solid #ccc; margin-bottom: 1rem; padding: 1rem; border-radius: 8px;">
    <p>{post.content}</p>

    <div>
        <input 
            type="text" 
            placeholder="Add a compliment..." 
            bind:value={newComment} 
            on:keydown="{(e) => e.key === 'Enter' && submitComment()}" 
            style="width: 80%; margin-right: 5px;" 
        />
        <button on:click={submitComment}>Compliment</button>
    </div>

    {#if post.comments.length > 0}
        <div style="margin-top: 1rem;">
            <h4>Compliments:</h4>
            <ul>
                {#each post.comments as comment}
                    <li>{comment}</li>
                {/each}
            </ul>
        </div>
    {/if}
</div>
