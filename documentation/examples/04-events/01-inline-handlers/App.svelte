<script>
	let m = { x: 0, y: 0 };
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div on:mousemove={e => (m = { x: e.clientX, y: e.clientY })}>
	Le curseur se trouve à la position ({m.x} ; {m.y})
</div>

<style>
	div {
		width: 100%;
		height: 100%;
	}
</style>
