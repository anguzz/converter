<script>
    let gifUrl = '';
  
    async function convertToGif() {
      // add function to convert gif here 

    }
  </script>
  
  <main>
    <h1>Video to GIF Converter</h1>
    <input type="file" accept="video/*" id="videoInput" />
  
    <button on:click={convertToGif}>
      Convert to GIF
    </button>
  
    {#if gifUrl}
      <img src={gifUrl} alt="Converted GIF" />
    {/if}
  </main>
  