<script lang="ts">
  import { CloseCircleOutline, CubeOutline } from 'svelte-ionicons'
  import { iconSize, layoutSpace } from './constants'
  import type { ToolBarProps } from './types'

  let { colors, oncolor, color, onclear }: ToolBarProps = $props()
  const changeColor = (color: string) => () => oncolor(color)
</script>

<div class="tool__bar" style="--layout-space: {layoutSpace}px">
  {#each colors as _color}
    <button
      aria-label="color-btn"
      class="ink"
      style="
          background-color: {_color};
           box-shadow: {_color === color ? `0 0 14px ${color}` : 'none'}
        "
      onclick={changeColor(_color)}
    ></button>
  {/each}
  <div class="divider"></div>
  <button class="btn _warning">
    <CubeOutline size={iconSize} />
  </button>
  <button class="btn _danger" onclick={onclear}>
    <CloseCircleOutline size={iconSize} />
  </button>
</div>

<style>
  .tool__bar {
    position: fixed;
    left: 50%;
    bottom: var(--layout-space);
    transform: translateX(-50%);
    display: flex;
    align-items: 'center';
    gap: 10px;
  }

  .btn {
    height: var(--btn-size);
    width: var(--btn-size);
    border-radius: calc(var(--btn-size) / 4);
    cursor: pointer;
    font-size: 18px;
    outline: none;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  ._warning {
    background-color: rgba(253, 249, 216, 0.89);
    border: 1px solid #c7a548;
    color: #c7a548;
  }

  ._danger {
    background-color: #ffc0c0;
    border: 1px solid #e43f51;
    color: #e43f51;
  }

  .divider {
    height: var(--btn-size);
    width: 1px;
    background-color: var(--divider);
    border-radius: 999px;
  }

  .ink {
    height: var(--btn-size);
    width: var(--btn-size);
    border-radius: var(--btn-size);
    cursor: pointer;
  }
</style>
