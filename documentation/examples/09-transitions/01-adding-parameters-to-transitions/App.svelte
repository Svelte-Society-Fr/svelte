<script>
	import { fly } from 'svelte/transition';
	let visible = true;
</script>

<label>
	<input type="checkbox" bind:checked={visible} />
	visible
</label>

{#if visible}
	<p transition:fly={{ y: 200, duration: 2000 }}>Entre et sort en volant</p>
{/if}
