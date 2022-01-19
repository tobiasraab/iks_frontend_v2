<template>
  <div :id="'the_info_side'">
    <div :id="'years_container'">
      <div :id="'years_scale'">
        <h3
          v-for="element in steps"
          :key="element.name"

          :class="[{'active-year': (element.state === 'active')}, {'focus-year': (element.state === 'focus')}, {'passive-year': (element.state === 'passive')}]"
          :style="{'margin-top': element.margin + 'px'}"
        >
          {{ element.time }}
        </h3>
      </div>
    </div>
    <div :id="'info_container'">
      <div
        :id="'info_scale'"
      >
        <div
          v-for="element in steps"
          :key="element.name"

          :style="{'height': 100 + 'vh'}"
        >
          <h1> {{ element.name }} </h1>
          <p :class="'info-text1'">
            {{ element.text1 }}
          </p>
          <h2> {{ element.heading2 }} </h2>
          <p :class="'info-text2'">
            {{ element.text2 }}
          </p>
        </div>
        <div>
          <h1> Anleitung </h1>
          <p :class="'info-text1'">
            So gehts: ...
          </p>
          <h2 />
          <p :class="'info-text2'" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheInfoSide',
  props: {
    data: {
      type: Object,
      default: null
    },
    steps: {
      type: Array,
      default: null
    }
  },
  data () {
    return {
    }
  },
  watch: {
    steps: {
      deep: true,
      handler () {
        this.setScale()
      }
    }
  },
  mounted () {
    this.setScale()
  },
  methods: {
    setScale () {
      let focus = false
      for (let i = 0; i < this.steps.length; i++) {
        if (this.steps[i].state === 'focus') {
          focus = true

          let marginYear = 337 + 30
          let marginInfo = 100

          for (let k = i; k >= 0; k--) {
            console.log(k)
            // add margin
            marginYear = marginYear - this.steps[k].margin - 30
            marginInfo = marginInfo - 100
            // add fontsize
          }
          document.getElementById('years_scale').style.top = marginYear + 'px'
          document.getElementById('info_scale').style.top = 'calc(' + marginInfo + '% + 337px)'
        }
      }
      if (!focus) {
        console.warn('else')
        const MARGININFO = -1200
        document.getElementById('info_scale').style.top = 'calc(' + MARGININFO + '% + 337px)'
      }
    }
  }
}
</script>

<style scoped>
  .active-year {
    color: white;
    font-family: 'frutigerregular';
    font-size: 20px;
  }
  .focus-year {
    color: #FF9B05;
    font-family: 'frutigermedium';
    font-size: 28px;
  }
  .passive-year {
    color: #424242;
    font-family: 'frutigerregular';
    font-size: 20px;
  }
  #the_info_side {
    width: 532px;
    height: 100vh;
    max-height: 100vh;
    position: absolute;
    display: inline-flex;
    right: 0;
    background-color: #424242;

    color: white
  }
  #years_container {
    width: 90px;
    max-height: 100vh;
    background-color: #747474;
    overflow: hidden;
  }
  #years_scale {
    position: relative;
    top: 0px;
    transition-duration: 2s;
    height: 100vh;
    max-height: 100vh;
  }
  #info_container {
    width: 442px;
    max-height: 100vh;
    background-color: #424242;
    margin-left: 18px;
    overflow: hidden;
  }
  #info_scale {
    position: relative;
    top: 0px;
    transition-duration: 2s;
    height: 100vh;
    max-height: 100vh;
  }
  h1 {
    color: #FF9B05;
    font-family: 'frutigermedium';
    font-size: 28px;
    margin-bottom: 38px;
  }
  .info-text1{
    color: white;
    font-family: 'frutigerregular';
    font-size: 20px;
    line-height: 24px;
  }
  h2 {
    color: white;
    font-family: 'frutigerregular';
    font-size: 20px;
    line-height: 24px;
    margin-top: 64px;
    margin-bottom: 6px;
    position: relative;
  }
  .info-text2{
    color: white;
    font-family: 'frutigermedium';
    font-size: 23px;
    line-height: 28px;
    position: relative;
  }
  h3 {
    position: relative;
    width: calc(100% - 15px);
    text-align: right;
  }
</style>
