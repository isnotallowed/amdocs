<template>
  <div class="panels">
    <div class="panels__wrapper">
      <Panel
        v-for="panel in panels"
        :id="panel.id"
        :key="panel.id"
        :title="panel.title"
        :intro="panel.intro"
        :category="panel.category"
        :details="panel.details"
        :is-favorite="panel.isFavorite"
        @toggleFavorite="toggleFavorite(panel.id, panel.isFavorite)"
        @click.native="currentPanel = panel"
      />
    </div>
    <transition name="slide">
      <PanelsRightSheet
        v-if="currentPanel"
        :id="currentPanel.id"
        :title="currentPanel.title"
        :intro="currentPanel.intro"
        :category="currentPanel.category"
        :details="currentPanel.details"
        :is-favorite="currentPanel.isFavorite"
        @closeRightSheet="currentPanel = null"
      />
    </transition>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      panels: [],
      currentPanel: null,
    }
  },
  async mounted() {
    const { data } = await this.$axios.get('/mock/api/panels.json')
    data.forEach((panel) => {
      const favoritePanels = JSON.parse(localStorage.getItem('panels'))
      if (favoritePanels) {
        if (favoritePanels.includes(panel.id)) {
          panel.isFavorite = true
        } else {
          panel.isFavorite = false
        }
      }
    })
    console.log(data)
    this.panels = data
  },
  methods: {
    toggleFavorite(id, status) {
      let favoritePanels = []
      if (localStorage.getItem('panels')) {
        favoritePanels = JSON.parse(localStorage.getItem('panels'))
      }
      this.panels.find((panel) => panel.id === id).isFavorite = !status
      if (status === false) {
        favoritePanels.push(id)
      } else {
        favoritePanels.splice(favoritePanels.indexOf(id), 1)
      }
      localStorage.setItem('panels', JSON.stringify(favoritePanels))
    },
  },
}
</script>
<style lang="scss" scoped>
.panels {
  max-width: 1240px;
  margin: 0 auto;
  &__wrapper {
    margin-top: 3rem;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 2rem;
  }
}
.slide-enter-active {
  transition: all 0.3s ease;
}
.slide-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-enter,
.slide-leave-to {
  transform: translateX(100%);
}
</style>
