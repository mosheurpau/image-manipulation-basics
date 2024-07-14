<script>
  export let imageSrc = "";
  let rotate = 0;
  let scale = 1;
  let grayscale = 0;
  let sepia = 0;
</script>

<div class="flex flex-col items-center space-y-4">
  {#if imageSrc}
    <img
      src={imageSrc}
      alt="LoadedImage"
      class="max-w-full h-auto w-full transform transition"
      style="
        transform: rotate({rotate}deg) scale({scale});
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
  </div>
</div>

<style>
  input[type="range"] {
    width: 100%;
  }
</style>
