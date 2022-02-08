<template>
  <div>
    <img :id="'map'" src="~/assets/images/background.png" alt="">
    <div id="info_blend_in">
      <img :id="'info_img'" :src="imagesrc" alt="" :class="'fade'">
      <div>
        <h2 :class="'fade'">
          {{ heading }}
        </h2>
        <p :class="'fade'">
          {{ text }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheBackground',
  props: {
    imagesrc: {
      type: String,
      default: null
    },
    heading: {
      type: String,
      default: null
    },
    text: {
      type: String,
      default: null
    },
    change: {
      type: Boolean,
      default: false
    }
  },
  watch: {
    change: {
      handler () {
        const FADECOLLECTION = document.getElementsByClassName('fade')
        if (this.change === true) {
          for (let i = 0; i < FADECOLLECTION.length; i++) {
            FADECOLLECTION[i].style.transitionDuration = 1 + 's'
            FADECOLLECTION[i].style.opacity = 0
          }
        } else {
          for (let i = 0; i < FADECOLLECTION.length; i++) {
            FADECOLLECTION[i].style.transitionDuration = 1 + 's'
            FADECOLLECTION[i].style.opacity = 1
          }
        }
      }
    }
  }
}
</script>

<style scoped>
  #map {
    position: absolute;
    left: 0;
    top: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
  }

  #info_blend_in{
    position: absolute;
    background-color: rgba(116, 116, 116, 0.7);
    top: 0;
    left: 0;
    width: 696px;
    height: 232px;
    margin: 36px;
    padding: 24px;
    display: inline-flex;
  }

  h2 {
    font-family: 'frutigerregular';
    opacity: 1;
    font-size: 16px;
    color: white;
    margin-left: 20px;
  }

  p{
    font-family: 'frutigerlight';
    font-size: 16px;
    color: white;
    margin-top: -12px;
    margin-left: 20px;
    white-space: pre-line;
  }

  #info_img{
    opacity: 1;
    max-height: 100%;
    max-width: 100%;
  }
</style>
