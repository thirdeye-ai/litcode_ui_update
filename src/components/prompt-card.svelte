<script lang="ts">
	import { Eye } from 'lucide-svelte';
	import * as Card from '$lib/components/ui/card';
	import { fade, scale, fly } from 'svelte/transition';
	import { spring } from 'svelte/motion';

	let { 
		title = "Fill out your vision",
		description = "Ask me any thing you need guidance on...",
		prompt = "ipsum dolor sit amet consectetur. Euismod porttitor dignissim",
		icon = Eye,
		onSelectPrompt
	} = $props();

	let isHovered = $state(false);

	async function handleClick() {
		onSelectPrompt?.(prompt, true);
	}
</script>
		<div 
			in:scale={{duration: 300}} 
			out:fade
			onmouseenter={() => isHovered = true}
			onmouseleave={() => isHovered = false}
			role="button"
			tabindex="0"
			class="transform transition-all duration-200 hover:scale-[1.02] hover:-translate-y-1 w-full"
		>
			<Card.Root 
				class="cursor-pointer p-2.5 md:p-3 bg-muted transition-all duration-200 hover:shadow-lg {isHovered ? 'bg-muted/80' : ''} min-h-[70px] md:min-h-[80px]" 
				onclick={handleClick}
			>
				<Card.Content class="space-y-1 md:space-y-2">
					<div 
						class="flex items-center gap-2 md:gap-4"
						in:fly={{y: 20, duration: 400, delay: 300}}
					>
						<div 
							class="p-1.5 md:p-2 rounded-lg bg-primary-foreground transition-transform duration-200 {isHovered ? 'scale-110' : ''}"
						>
							<svelte:component this={icon} class="w-3 h-3 md:w-4 md:h-4 text-foreground transition-transform duration-200 {isHovered ? 'rotate-12' : ''}" />
						</div>
						<Card.Title class="text-sm md:text-md font-normal line-clamp-2">{title}</Card.Title>
					</div>
				</Card.Content>
			</Card.Root>
		</div>
