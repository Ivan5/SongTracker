<template>
  <panel title="YouTube Video">
    <youtube :video-id="youtubeId" :player-width="400" :player-height="300" ></youtube>
  </panel>
</template>
<script>

import VueYouTubeEmbed from 'vue-youtube-embed'
export default {
  props:[
    'youtubeId'
  ],
}
</script>
<style>

</style>
