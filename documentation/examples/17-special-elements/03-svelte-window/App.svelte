<script>
	let key;
	let keyCode;

	function handleKeydown(event) {
		key = event.key;
		keyCode = event.keyCode;
	}
</script>

<svelte:window on:keydown={handleKeydown} />

<div style="text-align: center">
	{#if key}
		<kbd>{key === ' ' ? 'Espace' : key}</kbd>
		<p>{keyCode}</p>
	{:else}
		<p>Mettez le focus sur cette fenêtre et appuyez sur n'importe quelle touche</p>
	{/if}
</div>

<style>
	div {
		display: flex;
		height: 100%;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	kbd {
		background-color: #eee;
		border-radius: 4px;
		font-size: 6em;
		padding: 0.2em 0.5em;
		border-top: 5px solid rgba(255, 255, 255, 0.5);
		border-left: 5px solid rgba(255, 255, 255, 0.5);
		border-right: 5px solid rgba(0, 0, 0, 0.2);
		border-bottom: 5px solid rgba(0, 0, 0, 0.2);
		color: #555;
	}
</style>
