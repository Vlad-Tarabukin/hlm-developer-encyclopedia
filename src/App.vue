<script setup>
import Header from "@/components/Header.vue";
import SpritesTab from "@/components/SpritesTab.vue";
import ObjectsTab from "@/components/ObjectsTab.vue";
import SpriteInformationSidebar from "@/components/SpriteInformationSidebar.vue";
</script>

<script>
import sprites from "@/assets/info/sprites.json"

export default {
  data() {
    return {
      activeTab: "sprites"
    }
  },
  methods: {
    activateTab(tab) {
      this.activeTab = tab;
      this.setSprite(null)
    },
    setSprite(id) {
      this.$refs.spriteInformationSidebar.setSprite(sprites[id])
    }
  }
}
</script>

<template>
  <Header @tabchanged="activateTab"/>
  <main>
    <div class="content-list">
      <SpritesTab v-show="activeTab === 'sprites'" @changesprite="setSprite"/>
      <ObjectsTab v-show="activeTab === 'objects'" @changesprite="setSprite"/>
    </div>
    <SpriteInformationSidebar ref="spriteInformationSidebar" :sprite="null"/>
  </main>
</template>

<style scoped>
main {
  flex-grow: 1;
  display: flex;
  flex-flow: row;
  overflow: hidden;
}

.content-list {
  flex-grow: 1;
  height: 100%;
  overflow: auto;
}
</style>
