<script lang="ts">
    import { Carta } from 'carta-md';
    import 'carta-md/default.css';
    import { code } from '@cartamd/plugin-code';
    import '@cartamd/plugin-code/default.css';
    import DOMPurify from 'isomorphic-dompurify';
    import { onMount } from 'svelte';
    
    export let content: string;
    let renderedContent = '';
    
    const carta = new Carta({
        sanitizer: (html) => DOMPurify.sanitize(html),
        extensions: [
            code({
                theme: 'github-dark'
            })
        ]
    });

    $: {
        // Update rendered content whenever content prop changes
        updateContent(content);
    }

    async function updateContent(text: string) {
        try {
            // Wait for the render to complete
            renderedContent = await carta.render(text);
        } catch (error) {
            console.error('Error rendering markdown:', error);
            renderedContent = text; // Fallback to plain text
        }
    }
</script>

<div class="prose prose-invert max-w-none">
    {@html renderedContent}
</div>

<style>
    :global(.prose pre) {
        background-color: #1e1e1e;
        padding: 1rem;
        border-radius: 0.5rem;
        margin: 1rem 0;
    }
    
    :global(.prose code) {
        color: #e6e6e6;
        background-color: #2d2d2d;
        padding: 0.2rem 0.4rem;
        border-radius: 0.25rem;
    }

    /* Reset padding for code blocks inside pre */
    :global(.prose pre code) {
        padding: 0;
        background-color: transparent;
    }
</style>