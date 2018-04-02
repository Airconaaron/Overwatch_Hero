<template>
  <div class="hero" :style="skew">
    <div class="hero-portrait" :style="skew">
      <p class="score" :style="skew2"> {{score}} </p>
      <img class="icon" :src="url">
      <img class="role" :src="url2">
      <p class="name">{{name}}</p>
    </div>
  </div>
</template>

<script>
/* eslint-disable no-new */
import helper from '@/colours.js'
// console.log(helper.data)
export default {
  name: 'HeroPicker',
  props: {
    image: {
      type: String,
      default: 'logo.png'
    },
    name: {
      type: String,
      default: 'Hero'
    },
    role: {
      type: String,
      default: 'dps'
    },
    score: {
      type: Number,
      default: 50
    },
    left: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    url () {
      const url = require(`@/assets/${this.image}`)
      return url
    },
    url2 () {
      if (this.role === 'dps') {
        return require(`@/assets/class/offense.png`)
      } else if (this.role === 'def') {
        return require(`@/assets/class/defense.png`)
      } else if (this.role === 'tank') {
        return require(`@/assets/class/tank.png`)
      } else if (this.role === 'heal') {
        return require(`@/assets/class/support.png`)
      }
    },
    skew () {
      if (this.left) {
        return 'transform: translateX(-12%) translateY(-12%) skew(-0.11rad);'
      } else {
        return 'transform: translateX(-12%) translateY(-12%) skew(0.11rad);'
      }
    },
    skew2 () {
      if (this.left) {
        // console.log(helper.data.numberToColorHsl(0.3, 0, 1))
        return 'transform: skew(0.11rad); ' + 'color: ' + helper.data.numberToColorHsl(this.score / 100, 0, 1) + ';'
      } else {
        return 'transform: skew(-0.11rad); ' + 'color: ' + helper.data.numberToColorHsl(this.score / 100, 0, 1) + ';'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  margin-top: 0px;
}
.hero {
  background-color: rgba(51, 51, 51, 0.9);
  border-bottom: 3px solid #EFBA0B;
  border-top: 4px solid #EFBA0B;
  border-radius: 5px;
  float: left;
  padding-left: 15px;
  transform: translateX(-10%) translateY(-10%);
}
.icon {
    height: 100%;
    width: 100%;
    /* position: absolute; */
    right: 0;
    bottom: 0;
    margin: 10px 10px 5px 5px;
}

.hero-portrait {
    height: 90px;
    /* position: absolute; */
    right: 50%;
    width: 87.5px;
    cursor: pointer;
}
.name {
  text-align: center;
  transform: translateX(10%)
}
.score {
  position: absolute;
  top: 10%;
  /* left: 5%; */
  transform: translate(-0%, 0%);
  font-size: 25px;
  font-style: normal;
  font-weight: 900;
  -webkit-text-stroke-width: 0.5px;
  -webkit-text-stroke-color: white;
}

.role {
  position: absolute;
  width: 30px;
  -webkit-filter: drop-shadow(0 0 8px black);
  bottom:5%;
  transform: translateX(100%) translateY(50%);
}
</style>
