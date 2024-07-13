<script>
  import { onMount } from "svelte";
  import ImageDisplay from "./ImageDisplay.svelte";

  let imageSrc = "";

  function handleFileChange(event) {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        imageSrc = e.target.result;
      };
      reader.readAsDataURL(file);
    }
  }
</script>

<div class="container mx-auto p-4">
  <h1 class="text-2xl font-bold mb-4">Image Loader</h1>
  <input
    type="file"
    accept="image/*"
    on:change={handleFileChange}
    class="mb-4"
  />
  <ImageDisplay {imageSrc} />
</div>
