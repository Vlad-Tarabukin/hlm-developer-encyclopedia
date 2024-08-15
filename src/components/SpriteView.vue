<script>
export default {
  props: {
    sprite: Object
  },
  data() {
    return {
      imageSource: "",
      name: "sprRatPrisonDeadCut",
      size: {},
      center: {},
      mask: {},
      currentFrame: 0,
      showCenter: false,
      showMask: false
    }
  },
  methods: {
    setSprite(sprite, frame) {
      if (sprite != null) {
        this.imageSource = sprite.imageSource
        this.name = sprite.name
        this.size = sprite.size
        this.center = sprite.center
        this.mask = sprite.mask
        this.currentFrame = frame
      }
      else {
        this.imageSource = null
      }
    },
    centerStyle() {
      if (this.size.x > this.size.y) {
        let sizeRatio = this.$el.clientWidth / this.size.x
        return "margin-left: " + (this.center.x * sizeRatio - 8) + "px;" +
            "margin-top: " + (this.$el.clientWidth / 2 - (this.size.y / 2 - this.center.y) * sizeRatio - 8) + "px;"
      } else {
        let sizeRatio = this.$el.clientWidth / this.size.y
        return "margin-left: " + (this.$el.clientWidth / 2 - (this.size.x / 2 - this.center.x) * sizeRatio - 8) + "px;" +
            "margin-top: " + (this.center.y * sizeRatio - 8) + "px;"
      }
    },
    maskStyle() {
      if (this.size.x > this.size.y) {
        let sizeRatio = this.$el.clientWidth / this.size.x
        return "margin-left: " + (this.mask.x * sizeRatio) + "px;" +
            "margin-top: " + (this.$el.clientWidth / 2 - (this.size.y / 2 - this.mask.y) * sizeRatio - 1) + "px;" +
            "width: " + ((this.mask.size_x + 1) * sizeRatio - 2) + "px;" +
            "height: " + ((this.mask.size_y + 1) * sizeRatio - 1) + "px;"
      } else {
        let sizeRatio = this.$el.clientWidth / this.size.y
        return "margin-left: " + (this.$el.clientWidth / 2 - (this.size.x / 2 - this.mask.x) * sizeRatio) + "px;" +
            "margin-top: " + (this.mask.y * sizeRatio - 1) + "px;" +
            "width: " + ((this.mask.size_x + 1) * sizeRatio - 2) + "px;" +
            "height: " + ((this.mask.size_y + 1) * sizeRatio - 1) + "px;"
      }
    }
  },
  created() {
    this.setSprite(this.sprite, 0)
  }
}
</script>

<template>
  <div class="sprite-view" v-if="this.imageSource!= null">
    <img class="center" src="../assets/images/centerMarker.png" :style="centerStyle()" v-if="this.showCenter"/>
    <div class="mask" :style="maskStyle()" v-if="this.showMask"/>
    <img class="sprite" :src="'src/assets/images/sprites/' + imageSource + '/' + name + '/' + currentFrame + '.png'">
  </div>
</template>

<style scoped>
.sprite-view {
  margin: 25px 25px;
  border: lightgray solid 1px;
}

.sprite {
  width: 100%;
  height: 100%;
  object-fit: contain;
  z-index: 0;
  image-rendering: pixelated;
  background: white;
}

.mask {
  z-index: 1;
  position: absolute;
  border: blue solid 1px;
}

.center {
  z-index: 2;
  position: absolute;
  mix-blend-mode: difference;
}
</style>