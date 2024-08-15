<script>
import SpriteView from "@/components/SpriteView.vue";

export default {
  components: {SpriteView},
  data() {
    return {
      sprite: null,
      currentFrame: 0,
    }
  },
  methods: {
    setSprite(sprite) {
      this.sprite = sprite
      this.changeFrame(0)
    },
    changeFrame(frame) {
      this.currentFrame = frame
      this.$refs.spriteView.setSprite(this.sprite, frame)
    }
  }
}
</script>

<template>
  <div class="sprite-information-sidebar" v-show="sprite != null">
    <h1 class="sprite-information-sidebar-title">Sprite information</h1>
    <SpriteView ref="spriteView" style="width: 500px; height: 500px"/>
    <div class="frame-select" v-if="sprite != null && sprite.frames > 1">
      <input class="frame-slider" type="range" min="0" :max="sprite.frames - 1" :value="currentFrame"
             @input="changeFrame($event.target.value)">
      <input class="frame-number" type="number" min="0" :max="sprite.frames - 1" :value="currentFrame"
             @input="changeFrame($event.target.value)">
    </div>
    <div class="information-section" v-if="sprite != null">
      <p class="information-label"><strong>Name:</strong> {{ sprite.name }}</p>
      <p class="information-label"><strong>Id:</strong> {{ sprite.id }}</p>
      <p class="information-label"><strong>Source:</strong>
        <span style="text-align-all: justify">Atlases/{{ sprite.imageSource }}</span>
      </p>
      <p class="information-label"><strong>Frames:</strong> {{ sprite.frames }}</p>
      <p class="information-label"><strong>Size:</strong> {{ sprite.size.x }}; {{ sprite.size.y }}</p>
      <p class="information-label"><strong>Center:</strong> {{ sprite.center.x }}; {{ sprite.center.y }}
        <span style="padding-left: 35px">
          <input id="show-center" type="checkbox" @input="this.$refs.spriteView.showCenter = $event.target.checked">
          <label id="show-center">Show center</label>
        </span>
      </p>
      <p class="information-label"><strong>Mask:</strong>
        <span style="padding-left: 35px">
          <input id="show-mask" type="checkbox" @input="this.$refs.spriteView.showMask = $event.target.checked">
          <label id="show-mask">Show mask</label>
        </span>
        <br>X: {{ sprite.mask.x }} Width: {{ sprite.mask.size_x }}
        <br>Y: {{ sprite.mask.y }} Height: {{ sprite.mask.size_y }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.sprite-information-sidebar {
  position: sticky;
  top: 0;
  width: 550px;
  border-left: lightgray solid 1px;
  display: flex;
  flex-flow: column;
  align-items: center;
}

.sprite-information-sidebar-title {
  margin-bottom: 0;
  font-family: Retro Computer, monospace;
  font-size: 35px;
}

.frame-select {
  display: flex;
  flex-flow: row;
  width: 300px;
  height: 25px;
}

.frame-slider {
  flex-grow: 1;
}

.frame-number {
  font-family: monospace;
  font-size: 18px;
}

.information-section {
  width: 450px;
}

.information-label {
  word-break: break-all;
  white-space: normal;
  font-family: monospace;
  font-size: 24px;
}

.information-label strong {
  font-size: 26px;
}
</style>