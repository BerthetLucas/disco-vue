<script>
import LeftAside from './components/LeftAside.vue'
import MainDisplay from './components/MainDisplay.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    LeftAside,
    MainDisplay,
    Header,
    Footer
  },

  data() {
    return {
      filtreStock: false,
      filterState:null
    }
  },

  methods: {
    changeStockState(etat) {
      this.filtreStock = etat
      console.log(this.filtreStock)
    }, 
    changeFilterState(etat){
      this.filterState = etat
      console.log(this.filterState)
    }
  }
}
</script>

<template>
  <div>
    <Header />
    <div class="flex flex-row h-screen">
      <LeftAside @stock-only="changeStockState" @sort-filter="changeFilterState" />
      <MainDisplay :filtreStock="filtreStock" :filterState="filterState"/>
    </div>
    <Footer />
  </div>
</template>
