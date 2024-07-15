<script>
  export let imageSrc = "";
  let images = [];
  let newImageSrc = "";
  $: newImageSrc = imageSrc;

  function addImage() {
    if (newImageSrc) {
      images = [
        ...images,
        {
          id: Date.now(),
          src: newImageSrc,
          rotate: 0,
          scale: 1,
          grayscale: 0,
          sepia: 0,
          skewX: 0,
          skewY: 0,
          perspective: 500,
          rotateX: 0,
          zIndex: images.length, // Ensure each new image is layered above the previous ones
        },
      ];
      newImageSrc = "";
    }
  }

  function removeImage(id) {
    images = images.filter((image) => image.id !== id);
    updateZIndices();
  }

  function moveImageUp(id) {
    const index = images.findIndex((image) => image.id === id);
    if (index < images.length - 1) {
      const newImages = [...images];
      const temp = newImages[index];
      newImages[index] = newImages[index + 1];
      newImages[index + 1] = temp;
      images = newImages;
      updateZIndices();
    }
  }

  function moveImageDown(id) {
    const index = images.findIndex((image) => image.id === id);
    if (index > 0) {
      const newImages = [...images];
      const temp = newImages[index];
      newImages[index] = newImages[index - 1];
      newImages[index - 1] = temp;
      images = newImages;
      updateZIndices();
    }
  }

  function updateZIndices() {
    images = images.map((image, index) => ({ ...image, zIndex: index }));
  }
</script>

<div class="flex flex-col items-center space-y-4 p-4">
  <div class="flex flex-col md:flex-row md:space-x-2 w-full max-w-xl">
    <input
      type="text"
      placeholder="Image URL"
      bind:value={newImageSrc}
      class="border p-2 flex-grow mb-2 md:mb-0"
    />
    <button on:click={addImage} class="bg-blue-500 text-white p-2"
      >Add Image</button
    >
  </div>

  <div class="relative w-full max-w-4xl h-96 md:h-128 border overscroll-auto">
    {#each images as image (image.id)}
      <div
        class="absolute transform transition"
        style="
          z-index: {image.zIndex};
          transform: rotate({image.rotate}deg) scale({image.scale}) skew({image.skewX}deg, {image.skewY}deg) perspective({image.perspective}px) rotateX({image.rotateX}deg);
          filter: grayscale({image.grayscale}%) sepia({image.sepia}%);
        "
      >
        <img src={image.src} alt="LoadedImage" class="max-w-full h-auto" />
      </div>
    {/each}
  </div>

  <div class="flex flex-wrap justify-center gap-4 w-full">
    {#each images as image (image.id)}
      <div
        class="flex flex-col items-center space-y-2 border p-4 w-full sm:max-w-xs"
      >
        <img
          src={image.src}
          alt="LoadedImage"
          class="max-w-full h-auto w-full transform transition"
          style="
            transform: rotate({image.rotate}deg) scale({image.scale}) skew({image.skewX}deg, {image.skewY}deg) perspective({image.perspective}px) rotateX({image.rotateX}deg);
            filter: grayscale({image.grayscale}%) sepia({image.sepia}%);
          "
        />

        <button
          on:click={() => removeImage(image.id)}
          class="bg-red-500 text-white p-2">Remove</button
        >

        <button
          on:click={() => moveImageUp(image.id)}
          class="bg-green-500 text-white p-2">Move Up</button
        >

        <button
          on:click={() => moveImageDown(image.id)}
          class="bg-yellow-500 text-white p-2">Move Down</button
        >

        <div class="flex flex-col space-y-2 w-full">
          <label>
            Rotate:
            <input type="range" min="0" max="360" bind:value={image.rotate} />
          </label>
          <label>
            Grayscale:
            <input
              type="range"
              min="0"
              max="100"
              bind:value={image.grayscale}
            />
          </label>
          <label>
            Sepia:
            <input type="range" min="0" max="100" bind:value={image.sepia} />
          </label>
          <label>
            Skew X:
            <input type="range" min="-45" max="45" bind:value={image.skewX} />
          </label>
          <label>
            Skew Y:
            <input type="range" min="-45" max="45" bind:value={image.skewY} />
          </label>
          <label>
            Perspective:
            <input
              type="range"
              min="0"
              max="1000"
              bind:value={image.perspective}
            />
          </label>
          <label>
            Rotate X (3D):
            <input
              type="range"
              min="-180"
              max="180"
              bind:value={image.rotateX}
            />
          </label>
          <label>
            Scale:
            <input
              type="range"
              min="0.5"
              max="2"
              step="0.1"
              bind:value={image.scale}
            />
          </label>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  input[type="range"] {
    width: 100%;
  }
  .relative-container {
    position: relative;
    width: 100%;
    height: 600px;
  }
  .image-layer {
    position: absolute;
    top: 0;
    left: 0;
  }
</style>
