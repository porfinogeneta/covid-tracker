<template>
  <div v-if="state.isLoadnig">
    <Loading/>
  </div>
  <div v-else class="home">
    <div class="navbar">
      <Searcher :DataObject="state.data" @selected-country="ChangeSelectedCountry"/>
    </div>
    <CovidCases :GotData="state.selectedData"/>
  </div>

</template>

<script>
// @ is an alias to /src
import CovidCases from "@/components/CovidCases";
import Loading from "../views/Loading"
import {onMounted, reactive} from "vue";
import Searcher from '../components/Searcher.vue';

export default {
  name: 'Home',
  components: {
    CovidCases,
    Loading,
    Searcher,
  },
  setup() {

    const state = reactive({
      data: {},
      selectedData: {},
      isLoadnig: true,
      pathInAPI: 'Global'
    })

    onMounted(async () => {
      state.data = await FetchDataFromAPI();
      state.selectedData = state.data.Global
      state.isLoadnig = false
    })


    function ChangeSelectedCountry(payload) {
      state.selectedData = payload;
    }

    async function FetchDataFromAPI() {
      const response = await fetch('https://api.covid19api.com/summary')
      const data = await response.json()
      return data
    }

    return {
      state,
      ChangeSelectedCountry
    }
  }
}
</script>
<style scoped lang="scss">
.home {
  .navabr {
    display: flex;
    flex-direction: row;
  }
}
</style>
