<script>
  export let imageSrc = "";
</script>

{#if imageSrc}
  <img src={imageSrc} alt="LoadedImage" class="max-w-full h-auto" />
{:else}
  <p>No image loaded</p>
{/if}

<style>
  img {
    max-width: 100%;
    height: auto;
  }
</style>
