<script>
	import { count } from './stores.js';
	import Incrementer from './Incrementer.svelte';
	import Decrementer from './Decrementer.svelte';
	import Resetter from './Resetter.svelte';

	let countValue;

	const unsubscribe = count.subscribe((value) => {
		countValue = value;
	});
</script>

<h1>Le compteur vaut {countValue}</h1>

<Incrementer />
<Decrementer />
<Resetter />
