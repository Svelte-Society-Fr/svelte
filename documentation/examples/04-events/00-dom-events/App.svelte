<script>
	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div on:mousemove={handleMousemove}>
	Le curseur se trouve à la position ({m.x} ; {m.y})
</div>

<style>
	div {
		width: 100%;
		height: 100%;
	}
</style>
