<script lang="ts">
  import { Canvas } from '@threlte/core'
  import "./css/main.css"
  import Scene from './Scene.svelte'

</script>

<div id="text-container">
  <p id="text">Dirt Block from Minecraft</p>
</div>

<Canvas>
  <Scene />
</Canvas>

<style>
  *{
    margin: 0;
    padding: 0;
  }

  #text-container {
    position: absolute;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    background-color: rgba(0, 0, 0, 0.5);
    padding: 10px;
    border-radius: 5px;
    color: white;
    z-index: 999;
  }

  #text {
    margin: 0;
    font-size: 5vmin;
  }
</style>