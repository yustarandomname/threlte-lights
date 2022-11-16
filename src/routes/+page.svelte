<script>
	import { CircleGeometry, MeshStandardMaterial, BoxGeometry, DoubleSide } from 'three';
	import { DEG2RAD } from 'three/src/math/MathUtils';
	import { Canvas, Group, OrbitControls, PerspectiveCamera, T } from '@threlte/core';

	let flat = true;
	let linear = true;
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

		<T.AmbientLight intensity={1} />

		<!-- Cube -->
		<Group>
			<T.Mesh
				position.x={1}
				position.y={0.5}
				castShadow
				geometry={new BoxGeometry(1, 1, 1)}
				material={new MeshStandardMaterial({ color: '#E15F55' })}
			/>

			<T.Mesh position.x={-1} position.y={0.5}>
				<T.BoxGeometry args={[1, 2, 1]} />
				<T.MeshBasicMaterial color={'#308167'} />
			</T.Mesh>
		</Group>

		<!-- Floor -->
		<T.Mesh
			receiveShadow
			rotation.x={-90 * (Math.PI / 180)}
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
