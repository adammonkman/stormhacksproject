<script>
    export let disabled = false;
    export let highLighted = false;
    export let style = "";
</script>

<button class:disabled class:highLighted {disabled} on:click {style}>
    <slot />
</button>

<style>
    button {
        border: var(--focus) 2px solid;
        border-radius: 5px;
        color:black;
        background-color: white;
        padding: 0.4rem 0.5rem;
        margin: 0.25rem 0.25rem;
        font-family: sans-serif;
        transition: all ease-out 250ms;
    }

    button:hover {
        transform: scale(1.05);
        box-shadow: 0 0 10px 5px var(--fg0);
    }

    button:active {
        transform: scale(0.96);
        filter: brightness(0.95);
    }

    .disabled {
        filter: brightness(0.6);
        pointer-events: none;
    }

    .highLighted {
        border: var(--black) 2px solid;
    }
</style>