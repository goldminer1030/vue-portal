<template>
  <div id="VOD">
    <div class="backdrop" :style="{ 'background-image': 'url(' + content.banner_placeholder + ')' }">
      <div class="video-container" :style="{ 'background-image': displayVideo ? null : 'url(' + content.items[0].poster + ')' }">
        <div class="overlay">
          <div class="row">
            <div class="content" v-if="!displayVideo">
              <h2 class="title" v-if="content.items[0].programme">{{ content.items[0].programme }}</h2>
              <h3 class="subheading">{{ content.items[0].title }}</h3>
              <p>{{ content.items[0].description | truncateOnWord(200) }}</p>
              <div v-for="button in content.buttons">
                <ProButton
                  :target="button.target"
                  :background="button.background"
                  :color="button.color"
                  :text="button.text"
                  :context="context"
                  />
              </div>
              <p class="duration">
                <img src="../assets/icons/clock.png" />
                {{ content.items[0].duration | duration }}
              </p>
            </div>
            <div class="play-btn" v-on:click="displayVideo = true" v-if="!displayVideo"></div>
            <div class="main-video" v-if="displayVideo">
              <iframe class="video-player" src="http://st-rr-d.vidnt.com/player/?account=ipbc&width=100%&font_size=10&fullScreen=false&showEmbedded&qualityChange=true&&autoplay=true&playerType=videojs&videojsVersion=0.4.1.4&playback_url=http%3A%2F%2Fprotvstgmms.vidnt.com%2Fcontent%2Fprotvstg-SJ25C1-LO.1264-854x480.mp4" allowfullscreen></iframe>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="epg" :style="{ 'padding-top': displayVideo ? 0 : 'inherit' }">
      <div class="container">
        <ProCarousel :items="content.items" :grid="content.grid"/>
      </div>
    </div>
  </div>
</template>

<script>
import { duration, truncateOnWord } from '@/filters'
import ProCarousel from '@/components/ProCarousel'
import ProButton from '@/components/ProButton'
export default {
  name: 'VOD',
  components: {
    ProCarousel,
    ProButton
  },
  props: [
    'content',
    'context'
  ],
  data () {
    return {
      displayVideo: false
    }
  },
  filters: {
    duration,
    truncateOnWord
  }
}
</script>

<style scoped>
.backdrop {
  padding-left: 0;
  background-repeat: no-repeat;
  background-size: cover;
  margin-bottom: 50px;
}

.video-container {
  height: 450px;
  max-height: 600px;
  background-repeat: no-repeat;
  background-size: cover;
  margin: 0;
}

.video-container .overlay {
  position: relative;
  height: 100%;
  max-height: 600px;
  background: linear-gradient(to right, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.7));
}

.video-container .content {
  width: 250px;
  float: right;
  margin-right: 50px;
}

.video-container .title {
  font-size: 20px;
  border-bottom: 1px solid white;
  padding: 0 10px 10px 0;
  margin-right: 20px;
  text-transform: uppercase;
  font-weight: 200;
  padding-top:20px
}

.video-container .subheading {
  font-size: 25px;
  font-weight: 400;
}

.video-container p {
  font-size: 15px;
  margin: 0 20px 0 0;
  text-align: justify;
  font-weight: 400;
  line-height: 17px;
}

.video-container .more-videos-btn {
  opacity: 0.6;
  padding: 7px;
  background: #1f55ff;
  border: 1px solid white;
  max-width: 120px;
  font-size: 12px;
  color: white;
  text-align: center;
  margin-top: 10px;
  display: inline-block;
}

.video-container .more-videos-btn:hover {
  text-decoration: none;
  opacity: 1;
}

.video-container .play-btn {
  width: 100px;
  height: 100px;
  background: url('../assets/temp/main-video-play.png');
  opacity: 0.8;
  position: absolute;
  bottom: 30px;
  left: 30px;
}

.video-container .play-btn:hover {
  cursor: pointer;
  opacity: 1;
}

.epg {
  padding-top: 80px;
}

.main-video {
  position: relative;
  top: 0;
  height: 900px;
  overflow: hidden;
}

.video-player {
  border: 0;
  width: 100%;
  height: 100%;
}

.duration {
  display: block;
  margin-top: 30px !important;
}

</style>

<style lang="scss" scoped>
.row {
  @include media('<=tablet') {
    margin: 0;
  }
}
#VOD .container.backdrop {
  @include media('<=tablet') {
    height: 320px;
    background-image: none !important;
    width: 100%;
    padding: 0;
    margin-bottom: 20px;
  }
}
.video-container {
  @include media('<=tablet') {
    width: 100%;
    // height: 250px;
    // max-height: 250px;
    min-height: 1px;
    margin: 0;
    // .overlay {
    //   height: 250px;
    //   min-height: 1px;
    // }
    .content {
      margin-right: 5px;
      p {
        font-size: 10px;
        line-height: 11px;
        margin-bottom: 10px;
      }
      .duration {
        display: none;
      }
    }
  }
}
</style>
