<script lang="ts">
	import { useThrelteRoot } from '@threlte/core';

	export let flat = false;
	export let linear = false;

	const { flat: rootFlat, linear: rootLinear } = useThrelteRoot();

	$: {
		rootFlat.set(flat);
		rootLinear.set(linear);
	}
</script>
