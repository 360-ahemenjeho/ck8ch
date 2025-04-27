<script lang="ts">
  import { defaultIndicatorSize } from './constants'

  let { brushColor: color, brushSize: size } = $props()

  let canvas: any = $state(undefined)
  let context: any = $state()
  let coords: any = $state(null)

  export function clear() {
    context.clearRect(0, 0, canvas.width, canvas.height)
  }

  $effect(() => {
    context = canvas.getContext('2d')

    function resize() {
      canvas.width = window.visualViewport?.width || window.innerWidth
      canvas.height = window.visualViewport?.height || window.innerHeight
    }

    resize()

    window.visualViewport?.addEventListener('resize', resize)
    window.visualViewport?.addEventListener('scroll', resize)

    return () => {
      window.visualViewport?.removeEventListener('resize', resize)
      window.visualViewport?.removeEventListener('scroll', resize)
    }
  })
</script>

<canvas
  bind:this={canvas}
  onpointerdown={(e) => {
    coords = { x: e.offsetX, y: e.offsetY }

    context.fillStyle = color
    context.beginPath()
    context.arc(coords.x, coords.y, size / 2, 0, 2 * Math.PI)
    context.fill()
  }}
  onpointerleave={() => {
    coords = null
  }}
  onpointercancel={() => {
    coords = null
  }}
  onpointerup={() => {
    coords = null
  }}
  onpointermove={(e) => {
    if (e.buttons !== 1 || !coords) return

    e.preventDefault()

    const prevCoords = coords
    coords = { x: e.offsetX, y: e.offsetY }

    context.strokeStyle = color
    context.lineWidth = size
    context.imageSmoothingQuality = 'high'
    context.lineCap = 'round'
    context.lineJoin = 'round'
    context.beginPath()
    context.moveTo(prevCoords.x, prevCoords.y)
    context.lineTo(coords.x, coords.y)
    context.stroke()
  }}
></canvas>

{#if coords}
  <div
    class="indicator"
    style="
    background-color: {color}77;
    left: {coords.x - defaultIndicatorSize / 2}px;
    top: {coords.y - defaultIndicatorSize / 2}px;
    width: {defaultIndicatorSize}px;
    height: {defaultIndicatorSize}px;"
  >
    {size}
  </div>
{/if}

<style>
  .indicator {
    --size: 30px;
    height: var(--size);
    width: var(--size);
    position: absolute;
    border-radius: 999px;
    pointer-events: none;
    font-size: 11px;
    color: #ffffff;
    display: flex;
    align-items: center;
    justify-content: center;
    transform: translate(0, 0);
  }
</style>
