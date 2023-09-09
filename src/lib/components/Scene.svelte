<script>
  import { T, useFrame } from '@threlte/core'
  import { interactivity } from '@threlte/extras';
	import { cubicOut } from 'svelte/easing';
  import { spring } from 'svelte/motion';
  import { tweened } from 'svelte/motion';
  import dirt_texture from "../../lib/texture/s189772745713394276_p3856_i147_w750.jpeg"
  import { TextureLoader } from 'three';

  let rotation = 0;
  let scaleValue = 1;

  useFrame((state, delta) => {
    rotation += delta;
  });

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
  position={[10, 10, 10]}
  on:create={({ ref }) => {
    ref.lookAt(0, 1, 0);
  }}
/>

{#if $scale < (Math.max(window.innerWidth, window.innerHeight) / 2)}
  <T.Mesh
    scale={$scale}
    rotation.y={rotation}
  >
    <T.BoxGeometry />
    <T.MeshBasicMaterial map={texture} />
  </T.Mesh>
{/if}
