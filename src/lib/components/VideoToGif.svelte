<script>
  import { onMount } from 'svelte';
  import Whammy from 'whammy';

  let gifUrl = '';

  onMount(() => {
    const videoInput = document.getElementById('videoInput');
    const videoElement = document.createElement('video');
    const canvasElement = document.createElement('canvas');
    const ctx = canvasElement.getContext('2d');

    async function convertToGif() {
      // @ts-ignore
      const file = videoInput.files[0];

      if (!file) {
        console.error('No file selected');
        return;
      }

      const videoBlobUrl = URL.createObjectURL(file);
      videoElement.src = videoBlobUrl;

      await new Promise((resolve) => {
        videoElement.addEventListener('loadedmetadata', resolve);
      });

      canvasElement.width = videoElement.videoWidth;
      canvasElement.height = videoElement.videoHeight;

      // @ts-ignore
      const gifEncoder = new Whammy.Video();

      let currentTime = 0;

      while (currentTime < videoElement.duration) {
        videoElement.currentTime = currentTime;
        await new Promise((resolve) => {
          videoElement.addEventListener('seeked', resolve);
        });

        // @ts-ignore
        ctx.drawImage(videoElement, 0, 0, canvasElement.width, canvasElement.height);
        gifEncoder.add(canvasElement.toDataURL('image/webp'));

        currentTime += 0.1; // Adjust the frame capture interval here
      }

      const gifBlob = gifEncoder.compile();
      gifUrl = URL.createObjectURL(gifBlob);
    }

    // @ts-ignore
    document.getElementById('convertBtn').addEventListener('click', convertToGif);
  });
</script>

<main>
  <h1>Video to GIF Converter</h1>
  <input type="file" accept="video/*" id="videoInput" />
  <button id="convertBtn">Convert to GIF</button>
  
  {#if gifUrl}
    <img src={gifUrl} alt="Converted GIF" />
  {/if}
</main>
