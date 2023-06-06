<script>
    import Compressor from 'compressorjs';
  
    let compressedImageURL = '';
    let quality = 0.5;
    let originalFileSize = 0;
    let compressedFileSize = 0;
    
    
    function refreshPage() {
    location.reload();
  }
    async function compressImage(event) {
      const file = event.target.files[0];
  
      originalFileSize = Math.round(file.size / 1024); // convert to kb
  
      const compressor = new Compressor(file, {
        quality,
        success(result) {
          const reader = new FileReader();
          reader.readAsDataURL(result);
          reader.onloadend = () => {
            compressedImageURL = reader.result;
            const fileSizeInBytes = reader.result.length * 3 / 4;
            compressedFileSize = Math.round(fileSizeInBytes / 1024); // convert to kb
          };
        },
        error(err) {
          console.error('Image compression failed:', err.message);
        },
      });
  
      compressor.compress();
    }
  </script>
  
  <main>

    <h6 class="text-lg font-bold dark:text-white">Image Compressor</h6>
    <div class="slider-container">
        <label for="quality-slider">Image Quality: {quality}</label>
        <input
          type="range"
          id="quality-slider"
          min="0.1"
          max="1.0"
          step="0.1"
          bind:value={quality}
        />
      </div>

  

    <input class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded" type="file" accept="image/*" on:change={compressImage} />
    {#if compressedImageURL}

      <p>Original File Size: {originalFileSize} KB</p>
      <p>Compressed File Size: {compressedFileSize} KB</p>

      <button class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded"
       on:click={refreshPage}>restart</button>
      <img src="{compressedImageURL}" alt="Compressed Image" />
      

      {/if}
   
  
  
 
  </main>
  
  <style>
    .title{

    }
    .slider-container {
      margin-top: 10px;
      padding:10px;
    }
    .button{
        
    }
  </style>
  