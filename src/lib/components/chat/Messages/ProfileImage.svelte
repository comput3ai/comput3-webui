<script lang="ts">
	import { WEBUI_BASE_URL } from '$lib/constants';

	export let className = 'size-8';
	export let src = `${WEBUI_BASE_URL}/static/favicon.png`;
	
	// Determine if this is an AI/assistant message based on the source
	$: isAI = src?.includes('favicon.png') || src === '' || !src || src?.includes('static/');
	$: isUser = src?.includes('user.png') || src?.includes('gravatar.com') || src?.startsWith('data:');
</script>

{#if isAI}
	<div class="{className} flex items-center justify-center border-2 border-green-500 text-green-500 font-bold text-xs bg-black/80 font-mono cyberpunk-ai-avatar">
		AI
	</div>
{:else if isUser}
	<div class="{className} flex items-center justify-center border-2 border-orange-500 text-orange-500 font-bold text-xs bg-black/80 font-mono cyberpunk-user-avatar">
		U
	</div>
{:else}
	<!-- Custom profile image - still show image but make it square -->
	<img
		crossorigin="anonymous"
		aria-hidden="true"
		src={src}
		class="{className} object-cover border-2 border-orange-500 cyberpunk-profile"
		style="border-radius: 0 !important;"
		alt="profile"
		draggable="false"
	/>
{/if}
