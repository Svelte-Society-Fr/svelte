<script>
	let w;
	let h;
	let size = 42;
	let text = 'éditez-moi';
</script>

<input type="range" bind:value={size} />
<input bind:value={text} />

<p>taille: {w}px x {h}px</p>

<div bind:clientWidth={w} bind:clientHeight={h}>
	<span style="font-size: {size}px">{text}</span>
</div>

<style>
	input {
		display: block;
	}
	div {
		display: inline-block;
	}
</style>
