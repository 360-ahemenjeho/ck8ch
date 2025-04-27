<script lang="ts">
  import Canvas from './lib/Canvas.svelte'
  import { defaultColor } from './lib/constants'
  import SizeBar from './lib/SizeBar.svelte'
  import ToolBar from './lib/ToolBar.svelte'

  let canvas: any

  const colors: string[] = ['#ff0000', '#0000ff', '#008000']
  let size = $state(4)
  let color: string = $state(defaultColor)

  const changeColor = (_color: string) => (color = _color)
  const clearCanvas = () => {
    const res = window.confirm('Are you sure you want to `clear` canvas?')
    if (!res) return
    canvas.clear()
  }
</script>

<section class="wrapper">
  <Canvas bind:this={canvas} brushColor={color} brushSize={size} />
  <ToolBar {colors} {color} oncolor={changeColor} onclear={clearCanvas} />
  <SizeBar bind:size />
</section>

<style>
  .wrapper {
    height: 100vh;
    width: 100vw;
    position: relative;
    overflow: hidden;
  }
</style>
