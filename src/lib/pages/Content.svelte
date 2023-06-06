<script lang="ts">
  import Link from "$lib/components/Link.svelte";
  import Page from "$lib/components/Page.svelte";
  import Text from "$lib/components/Text.svelte";
  import { primaryBackground } from "$lib/utils/constants";

  export let backgroundClass = primaryBackground;
  import VideoToGif from "$lib/components/VideoToGif.svelte";
  import ImageCompressor from "$lib/components/ImageCompressor.svelte";

</script>

<Page id="content" title=" " {backgroundClass}>
  <Text>

    <ImageCompressor/>
    <!--not func yet <VideoToGif/> -->


  </Text>
</Page>


<style>
  
</style>

