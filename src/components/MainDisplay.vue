<script>
import { records } from '../data/allRecords'

export default {
  name: 'MainDisplay',
  props: {
    filtreStock: {
      type: Boolean
    },
    filterState: {
      type: String
    }
  },
  data() {
    return {
      table: records,
      newTab: null,
    }
  },
  computed: {
    filtreStockAction() {
      console.warn('Wesh', this.filtreStock)
      this.newTab = this.table // Initialisez newTab avec le tableau d'origine

      if (this.filtreStock) {
        console.log('hello')

        // Utilisez la méthode filter pour créer un nouveau tableau filtré
        this.newTab = this.table.filter(function (item) {
          return item.stock > 0
        })
      }

      if (this.filterState === 'year') {
        this.newTab = this.table.sort((a, b) => a.year - b.year)
      } else if (this.filterState === 'pitchfork') {
        this.newTab = this.table.sort((a, b) => a.pitchforkPos - b.pitchforkPos)
      }

      console.log(this.newTab)
      return this.newTab
    }, 

    addStock(item){
        console.log(item)
        item.stock = item.stock + 1; 
    }
  }
}
</script>

<template>
  <section class="text-gray-600 body-font">
    <!-- one records -->
    <div class="container px-5 mx-auto">
      <div
        v-for="item in filtreStockAction"
        :key="item.id"
        class="p-5 bg-white flex items-center mx-auto border-b shadow-md mb-10 border-gray-400 rounded-lg sm:flex-row flex-col"
      >
        <div
          class="sm:w-44 sm:h-44 lg:w-40 lg:h-40 sm:mr-10 inline-flex items-center justify-center flex-shrink-0"
        >
          <img :src="item.coverUrl !== '' ? item.coverUrl : '../src/img/default.jpg'" />
        </div>
        <!-- Card -->
        <div class="flex-grow sm:text-left text-center mt-6 sm:mt-0">
          <h1 class="text-black text-2xl title-font font-bold mb-2">
            {{ item.title }}
          </h1>
          <h3 class="text-black text-xl title-font mb-2">
            {{ item.artist }}<span class="font-light mr-2"> {{ item.year }}</span>
          </h3>
          <p class="leading-relaxed text-base">
            {{ item.comment }}
          </p>
          <div class="py-4">
            <div class="inline-block mr-2">
              <!-- quand le stock est ok  -->
              <div v-if="item.stock > 0" class="flex pr-2 h-full items-center">
                <svg
                  class="text-green-500 w-6 h-6 mr-1"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                  stroke="currentColor"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path stroke="none" d="M0 0h24v24H0z" />
                  <circle cx="12" cy="12" r="9" />
                  <path d="M9 12l2 2l4 -4" />
                </svg>
                <p class="title-font font-medium">{{ item.stock }}</p>
              </div>
            </div>
            <div class="inline-block mr-2">
              <!-- quand le stock est à zéro  -->
              <div v-if="item.stock <= 0" class="flex pr-2 h-full items-center">
                <svg
                  class="text-gray-500 w-6 h-6 mr-1"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <circle cx="12" cy="12" r="10"></circle>
                  <line x1="15" y1="9" x2="9" y2="15"></line>
                  <line x1="9" y1="9" x2="15" y2="15"></line>
                </svg>
                <p class="title-font font-medium">out of stock</p>
              </div>
            </div>
          </div>
          <div class="md:flex font-bold text-gray-800">
            <div class="w-full md:w-1/2 flex space-x-3">
              <div class="w-1/2">
                <p>pitchfork pos : #28</p>
                <!-- pitchfork pos  -->
              </div>
            </div>
            <div class="w-full">
              <div class="float-right">
                <button
                  type="button"
                  class="border border-teal-500 bg-teal-500 text-white rounded-md px-4 py-2 m-2 ease select-none hover:bg-teal-400"
                  @click="item.stock++"
                >
                  +
                </button>
                <button
                  type="button"
                  class="border border-teal-500 bg-teal-500 text-white rounded-md px-4 py-2 m-2 ease select-none hover:bg-purple-800"
                  :disabled="item.stock == 0 ? true : false"
                  @click="item.stock--"
                >
                  -
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!-- end one records -->
</template>
