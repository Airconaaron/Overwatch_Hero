<template>
  <div class="map">
    <div class="map-thumb">
      <img class="icon" :src="url">
      <p class="name">{{name}}</p>
    </div>
  </div>
</template>

<script>
/* eslint-disable no-new */
export default {
  name: 'Map',
  props: {
    image: {
      type: String,
      default: 'logo.png'
    },
    name: {
      type: String,
      default: 'None'
    }
  },
  computed: {
    url () {
      const url = require(`@/assets/${this.image}`)
      return url
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  margin: 0px;
  position: absolute;
  text-align: center;
  bottom: -40px;
  left: 20px;
}
.map {
  border-radius: 7px;
  width: 140px;
  height: 85px;
  border-left: 3px solid #EFBA0B;
  border-right: 3px solid #EFBA0B;
  position: relative;
  cursor: pointer;
  margin: 20px 5px;
}
.icon {
    height: 100%;
    width: 100%;
    /* position: absolute; */
    right: 0;
    bottom: 0;
    margin: 10px;
    transform: translateX(-7.5%) translateY(-11%)
}

/* .hero-portrait {
    height: 90px;
    position: absolute;
    right: 50%;
    width: 87.5px;
    cursor: pointer;
} */

</style>
