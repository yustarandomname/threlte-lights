<script>
	import { CircleGeometry, MeshStandardMaterial, BoxGeometry, DoubleSide } from 'three';
	import { DEG2RAD } from 'three/src/math/MathUtils';
	import {
		AmbientLight,
		Canvas,
		Group,
		Mesh,
		OrbitControls,
		PerspectiveCamera
	} from '@threlte/core';
	import { spring } from 'svelte/motion';
	import SetRoot from './SetRoot.svelte';

	const scale = spring(1);

	let flat = false;
	let linear = false;
</script>

<div class="scene" style="height: 30rem; border: 1px solid black; border-radius: 1rem">
	<Canvas {flat} {linear}>

		<PerspectiveCamera position={{ x: 10, y: 10, z: 10 }} fov={24}>
			<OrbitControls
				maxPolarAngle={DEG2RAD * 80}
				autoRotate={false}
				enableZoom={false}
				target={{ y: 0.5 }}
			/>
		</PerspectiveCamera>

		<AmbientLight intensity={1} />

		<!-- Cube -->
		<Group scale={$scale}>
			<Mesh
				interactive
				on:pointerenter={() => ($scale = 2)}
				on:pointerleave={() => ($scale = 1)}
				position={{ x: 1, y: 0.5 }}
				castShadow
				geometry={new BoxGeometry(1, 1, 1)}
				material={new MeshStandardMaterial({ color: '#E15F55' })}
			/>

			<Mesh
				interactive
				on:pointerenter={() => ($scale = 2)}
				on:pointerleave={() => ($scale = 1)}
				position={{ x: -1, y: 0.5 }}
				castShadow
				geometry={new BoxGeometry(1, 1, 1)}
				material={new MeshStandardMaterial({ color: '#308167' })}
			/>
		</Group>

		<!-- Floor -->
		<Mesh
			receiveShadow
			rotation={{ x: -90 * (Math.PI / 180) }}
			geometry={new CircleGeometry(3, 72)}
			material={new MeshStandardMaterial({ side: DoubleSide, color: '#ccc' })}
		/>
	</Canvas>
</div>

<h2>Toggle <code>useThrelteRoot({`{flat: ${flat}, linear: ${linear}}`})</code></h2>
<button on:click={() => (flat = !flat)}>Toggle flat to {!flat}</button>
<button on:click={() => (linear = !linear)}>Toggle linear to {!linear}</button>

<h2>Reference</h2>
<div class="reference" style="background: #E15F55" />
<div class="reference" style="background: #308167" />

<style>
	.scene {
		height: 30rem;
		width: 100%;
	}

	.reference {
		margin: 1rem;
		height: 10rem;
		width: 10rem;
	}
</style>
