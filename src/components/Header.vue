<script>
export default {
  emits: ["tabchanged"],
  data() {
    return {
      tabs: ["sprites", "objects"],
      selectedTab: 0
    }
  },
  methods: {
    selectTab(index) {
      this.selectedTab = index
      this.$emit('tabchanged', this.tabs[index])
    }
  }
}
</script>

<template>
  <header>
    <h1 class="title">"Hotline Miami 2: Wrong Number" developer encyclopedia</h1>
    <div class="tab-menu">
      <button v-for="(tab, index) in tabs" :class="'tab-button' + (selectedTab === index ? ' selected' : '')"
              @click="selectTab(index)">{{ tab }}
      </button>
    </div>
  </header>
</template>

<style scoped>
header {
  padding: 0 0 25px 0;
  background-image: linear-gradient(45deg in oklab, #0081be, #8500c7);
}

.title {
  margin: 0 0 20px 0;
  padding: 20px 0 10px 20px;
  color: #fffa00;
  font-family: Justice Out, monospace;
  font-size: 40px;
  text-shadow: 2px 2px #c58d00;
  letter-spacing: 6px;
}

.tab-button {
  display: inline-block;
  margin: 0 0 0 15px;
  background: none;
  border: none;
  color: #ffff00;
  font-family: Retro Computer, monospace;
  font-size: 24px;
  text-shadow: 3px 3px rgba(17, 17, 17, 0.5);
  text-underline-offset: 5px;
}

.tab-button.selected {
  text-decoration: underline 4px;
  text-underline-offset: 7px;
}

.tab-button:hover {
  transform: translateY(-3px);
}
</style>