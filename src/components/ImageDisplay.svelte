<script>
  export let imageSrc = "";
  let rotate = 0;
  let scale = 1;
  let grayscale = 0;
  let sepia = 0;
  let skewX = 0;
  let skewY = 0;
  let perspective = 500;
  let rotateX = 0;
</script>

<div class="flex flex-col items-center space-y-4">
  {#if imageSrc}
    <img
      src={imageSrc}
      alt="LoadedImage"
      class="max-w-full h-auto w-full transform transition"
      style="
        transform: rotate({rotate}deg) scale({scale}) skew({skewX}deg, {skewY}deg) perspective({perspective}px) rotateX({rotateX}deg);
        filter: grayscale({grayscale}%) sepia({sepia}%);
      "
    />
  {:else}
    <p>No image loaded</p>
  {/if}

  <div class="flex flex-col space-y-2">
    <label>
      Rotate:
      <input type="range" min="0" max="360" bind:value={rotate} />
    </label>
    <label>
      Scale:
      <input type="range" min="0.5" max="2" step="0.1" bind:value={scale} />
    </label>
    <label>
      Grayscale:
      <input type="range" min="0" max="100" bind:value={grayscale} />
    </label>
    <label>
      Sepia:
      <input type="range" min="0" max="100" bind:value={sepia} />
    </label>
    <label>
      Skew X:
      <input type="range" min="-45" max="45" bind:value={skewX} />
    </label>
    <label>
      Skew Y:
      <input type="range" min="-45" max="45" bind:value={skewY} />
    </label>
    <label>
      Perspective:
      <input type="range" min="0" max="1000" bind:value={perspective} />
    </label>
    <label>
      Rotate X (3D):
      <input type="range" min="-180" max="180" bind:value={rotateX} />
    </label>
  </div>
</div>

<style>
  input[type="range"] {
    width: 100%;
  }
</style>
