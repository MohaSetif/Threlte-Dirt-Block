<script lang="ts">
  import { T, useFrame } from '@threlte/core'
  import { ContactShadows, Float, OrbitControls, interactivity } from '@threlte/extras';
	import { cubicOut } from 'svelte/easing';
  import { spring } from 'svelte/motion';
  import { tweened } from 'svelte/motion';
  import dirt_texture from "../../lib/texture/s189772745713394276_p3856_i147_w750.jpeg"
  import { BoxGeometry, TextureLoader } from 'three';

  let scaleValue = 1;

  let pos = {
    x: 0
  }
  useFrame(() => {
    pos.x = Math.sin(Date.now() / 2000)
  })

  interactivity();

  //Smooth scrolling animation
  const scale = tweened(scaleValue, { duration: 300, easing: cubicOut });

  function handleScroll(event) {
    const maxScale = Math.max(window.innerWidth, window.innerHeight) / 2;

    if (event.deltaY < 0) {
      //Scroll up, make the cube bigger
      scaleValue += 0.1;
    } else {
      //Scroll down, make the cube smaller
      scaleValue -= 0.1;
    }
    
    // Limit the scale value
    scaleValue = Math.max(1, Math.min(maxScale, scaleValue));
    //Update the scale tweened store
    scale.set(scaleValue);
  }

  const textureLoader = new TextureLoader();
  const texture = textureLoader.load(dirt_texture);
</script>

<svelte:window on:wheel={handleScroll} />

<T.PerspectiveCamera
  makeDefault
  position={[10, 5, 5]}
  fov={25}
>
  <OrbitControls
    enabled={false}
    autoRotate
    autoRotateSpeed={0.5}
    target.y={1}
  />
</T.PerspectiveCamera>
<T.DirectionalLight
  intensity={0.8}
  position.x={5}
  position.y={10}
/>
<T.AmbientLight intensity={0.2} />

<ContactShadows
  opacity={1}
  scale={10}
  blur={1}
  far={10}
  resolution={256}
  color="#000000"
/>

{#if $scale < (Math.max(window.innerWidth, window.innerHeight) / 2)}
<Float
  floatIntensity={5}
  scale={$scale}
>
  <T.Mesh
    scale={$scale}
  >
    <T.BoxGeometry />
    <T.MeshBasicMaterial map={texture} />
  </T.Mesh>
  </Float>
{/if}
