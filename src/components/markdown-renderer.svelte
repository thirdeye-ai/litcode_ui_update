<script lang="ts">
    import Markdown from 'svelte-exmarkdown';
    import { gfmPlugin } from 'svelte-exmarkdown/gfm';
    
    let props = $props<{ content: string }>();
    const plugins = [gfmPlugin()];
</script>

<div class="prose prose-invert max-w-none">
    <Markdown md={props.content} {plugins} />
</div>

<style>
    :global(.prose pre) {
        background-color: rgb(30, 30, 30);
        border-radius: 0.5rem;
        padding: 1rem;
        margin: 1rem 0;
    }

    :global(.prose code) {
        background-color: rgb(30, 30, 30);
        padding: 0.2rem 0.4rem;
        border-radius: 0.25rem;
        font-size: 0.875em;
        color: rgb(230, 230, 230) !important;
    }

    :global(.prose pre code) {
        background-color: transparent;
        padding: 0;
        border-radius: 0;
        color: #ffffff !important;
        white-space: pre-wrap;
        word-break: break-word;
    }

    :global(.prose pre) {
        overflow-x: auto;
        max-width: 100%;
    }
</style>
