<template>
  <div class="w-screen h-screen text-center">
    <video
      id="player"
      controls
      muted
      class="cld-video-player w-2/3 h-2/3 mx-auto my-20"
      autoplay
    >
    </video>
    Videos by cottonbro from Pexels
  </div>
</template>

<script>
export default {
  data(){
    return {
      player:null,
      mainSouce: "nuxtjs-interactive-videos/pexels-cottonbro-10678925",
      clickSources:{
        man: "nuxtjs-interactive-videos/pexels-cottonbro-10679050",
        woman: "nuxtjs-interactive-videos/pexels-cottonbro-10678927",
        grass: "nuxtjs-interactive-videos/pexels-cottonbro-10678930",
      }
    };
  },
  mounted(){
    this.player = cloudinary.videoPlayer(
      'player',
      {
        cloud_name: process.env.NUXT_ENV_CLOUDINARY_CLOUD_NAME,
        transformations: {
          quality: 50
        }
      }
    );

    this.player.source(
      this.mainSouce,
      {
        interactionAreas: {
          enable: true,
          template: [
            {
                left : 35,
                top: 50,
                width: 20,
                height: 20,
                id: 'man'
            },
            {
                left : 50,
                top: 50,
                width: 20,
                height : 20,
                id: 'woman'
            },
            {
                left : 40,
                top: 70,
                width: 20,
                height : 20,
                id: 'grass'
            }
          ],
          onClick: (event) => event.zoom(this.clickSources[event.item.id])
        }
      });
  }
}
</script>
