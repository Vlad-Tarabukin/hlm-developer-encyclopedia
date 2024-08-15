<script>
import spritesJson from "@/assets/info/sprites.json"
import SpriteView from "@/components/SpriteView.vue";
import SpriteInformationSidebar from "@/components/SpriteInformationSidebar.vue";
export default {
  components: {SpriteInformationSidebar, SpriteView},
  emits: ["changesprite"],
  data() {
    return {
      sprites: spritesJson
    }
  }
}
</script>

<template>
  <div class="tab-main">
    <table class="tab-table">
      <tr class="table-hint first-row">
        <th rowspan="2"/>
        <th rowspan="2">Name</th>
        <th rowspan="2">Id</th>
        <th rowspan="2" style="width: 10px;">Source</th>
        <th rowspan="2">Frames</th>
        <th colspan="2">Size</th>
        <th colspan="2">Center</th>
        <th colspan="4">Mask</th>
      </tr>
      <tr class="table-hint second-row">
        <th>X</th>
        <th>Y</th>
        <th>X</th>
        <th>Y</th>
        <th>X</th>
        <th>Y</th>
        <th>Width</th>
        <th>Height</th>
      </tr>
      <tr v-for="(sprite, key) in sprites">
        <td><SpriteView :sprite="sprites[key]" style="width: 50px; height: 50px;" @click="this.$emit('changesprite', key)"/></td>
        <td>{{sprite.name}}</td>
        <td class="table-align-center">{{sprite.id}}</td>
        <td>Atlases/{{sprite.imageSource}}</td>
        <td class="table-align-center">{{sprite.frames}}</td>
        <td class="table-align-center">{{sprite.size.x}}</td>
        <td class="table-align-center">{{sprite.size.y}}</td>
        <td class="table-align-center">{{sprite.center.x}}</td>
        <td class="table-align-center">{{sprite.center.y}}</td>
        <td class="table-align-center">{{sprite.mask.x}}</td>
        <td class="table-align-center">{{sprite.mask.y}}</td>
        <td class="table-align-center">{{sprite.mask.size_x}}</td>
        <td class="table-align-center">{{sprite.mask.size_y}}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped>
.tab-table {
  font-size: 20px;
  font-family: monospace;
  overflow: scroll;
  height: 100%;
}
.table-hint {
  position: sticky;
  font-weight: bold;
  background: white;
}
.table-hint.first-row {
  top: 0;
  height: 25px;
}
.table-hint.second-row {
  top: 25px;
  height: 35px;
}
.table-hint th {
  padding: 0 25px 0 25px;
}
.table-align-center {
  text-align: center;
}
</style>