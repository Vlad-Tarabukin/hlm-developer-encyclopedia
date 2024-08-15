<script>
import objectsJson from "@/assets/info/objects.json"
import spritesJson from "@/assets/info/sprites.json"
import SpriteView from "@/components/SpriteView.vue";

export default {
  components: {SpriteView},
  emits: ["changesprite"],
  data() {
    return {
      objects: objectsJson,
      sprites: spritesJson
    }
  }
}
</script>

<template>
  <div class="tab-main">
    <table class="tab-table">
      <tr class="table-hint">
        <th/>
        <th>Name</th>
        <th>Id</th>
        <th>Sprite Id<br><u>-1</u> - No<br>sprite</th>
        <th>Depth</th>
        <th>Parent Object Id<br><u>-100</u> - No<br>parent</th>
        <th>Mask Sprite Id<br><u>-1</u> - Same as<br>sprite</th>
        <th>Solid</th>
        <th>Visible</th>
        <th>Persistent</th>
      </tr>
      <tr class="table-data" v-for="object in objects">
        <td v-if="object.sprite_id !== -1">
          <SpriteView :sprite="sprites[object.sprite_id]" style="width: 50px; height: 50px;"
                      @click="this.$emit('changesprite', object.sprite_id)"/>
        </td>
        <td class="table-align-center" v-else><img style="image-rendering: pixelated" src="/src/assets/images/noSprite.png"></td>
        <td>{{ object.name }}</td>
        <td class="table-align-center">{{ object.id }}</td>
        <td class="table-align-center" v-if="object.sprite_id !== -1"
            @click="this.$emit('changesprite', object.sprite_id)"><u>{{ object.sprite_id }}</u>
        </td>
        <td class="table-align-center" v-else>-1</td>
        <td class="table-align-center">{{ object.depth }}</td>
        <td class="table-align-center" v-if="object.parent !== -100">{{ object.parent }}</td>
        <td class="table-align-center" v-else>-100</td>
        <td class="table-align-center" v-if="object.mask_sprite_id !== -1"
            @click="this.$emit('changesprite', object.mask_sprite_id)"><u>{{ object.mask_sprite_id }}</u>
        </td>
        <td class="table-align-center" v-else>-1</td>
        <td class="table-align-center" v-if="object.solid">Yes</td>
        <td class="table-align-center" v-else>No</td>
        <td class="table-align-center" v-if="object.visible">Yes</td>
        <td class="table-align-center" v-else>No</td>
        <td class="table-align-center" v-if="object.persistent">Yes</td>
        <td class="table-align-center" v-else>No</td>
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
  top: 0;
  height: 55px;
}

.table-hint th {
  padding: 0 25px 0 25px;
}

.table-align-center {
  text-align: center;
}

.table-data {
  height: 105px;
}
</style>