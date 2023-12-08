<script>
export default {
  name: 'LeftAside',
  emits: ['stock-only','sort-filter'],

  data() {
    return {
      checkBox: false, 
      selected: null
    }
  },

  methods: {
    stockFilter() {
  
        this.$emit('stock-only', this.checkBox)
        // console.log(this.checkBox)
      
    }, 
    sortFilter(){
      this.$emit('sort-filter', this.selected)
      // console.log(this.selected)
    }
  }
}

</script>

<template>
  <div class="flex flex-row">
    <div class="px-8 bg-cyan-100">
      <!-- left filter panel -->
      <div class="mt-2 basis-1/4">
        <div class="overflow-hidden shadow sm:rounded-md">
          <div class="bg-white p-6 w-64 h-96">
            <fieldset>
              <legend class="sr-only">Filtres</legend>
              <div class="text-base font-medium text-gray-900" aria-hidden="true">Filtres</div>
              <div class="mt-4 space-y-4">
                <div class="flex items-start">
                  <div class="flex h-5 items-center">
                    <input
                      id="comments"
                      name="comments"
                      type="checkbox"
                      class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
                      v-model="checkBox"
                      @change="stockFilter"
                    />
                  </div>
                  <div class="ml-3 text-sm">
                    <label for="comments" class="font-medium text-cyan-700">In stock only</label>
                  </div>
                </div>
              </div>
              <label for="sortBy" class="block text-sm mt-2 font-medium text-cyan-700"
                >Sort by</label
              >
              <select
                id="sortBy"
                name="sortBy"
                autocomplete="country-name"
                class="mt-1 block w-full rounded-md border border-gray-300 bg-white py-2 px-3 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm"
                v-model="selected"
                @change="sortFilter"

              >
                <option value="year">Year</option>
                <option value="pitchfork">Pitchfork</option>
              </select>
            </fieldset>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
