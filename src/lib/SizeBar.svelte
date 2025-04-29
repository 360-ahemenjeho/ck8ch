<script>
  import { layoutSpace } from './constants'

  let { size = $bindable() } = $props()
</script>

<div class="size__bar" style="--layout-space: {layoutSpace}px">
  <input
    type="range"
    bind:value={size}
    min="1"
    max="100"
    class="size__slider"
    id="slider"
  />
</div>

<style>
  .size__bar {
    position: fixed;
    left: 50%;
    top: var(--layout-space);
    transform: translateX(-50%);
  }

  .size__slider {
    -webkit-appearance: none;
    appearance: none;
    height: var(--slider-size);
    background-color: var(--fg);
    border-radius: 999px;
    outline: none;
    box-shadow: none;
    border: none;
  }

  .size__slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    height: calc(var(--slider-size) * 2.5);
    width: calc(var(--slider-size) * 2.5);
    border-radius: 999px;
    background-color: var(--slider-thumb);
    cursor: pointer;
    transition: all 0.2s ease;
  }
</style>
