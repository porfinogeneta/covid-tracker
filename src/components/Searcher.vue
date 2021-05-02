<template>
  <section class="container">
    <label class="title">Choose a country:</label>
    <select class="select" @change="PassSelectedCountry()" v-model="state.selected">
      <option value="Global">Global Data</option>
      <option v-for="country in GetData.Countries" :key="country.ID">
        {{country.Country}}
      </option>
    </select>
  </section>
  
</template>

<script>
import {computed, reactive} from 'vue'

export default {
  name: "Searcher",
  props: {
    DataObject: {
      requiered: true
    }
  },
  emits: ['selected-country'],
  setup(props, {emit}) {

    const state = reactive({
      selected: '',
      dataList: []
    })

    const GetData = computed(() => {
      return props.DataObject
    })

    const PassSelectedCountry = () => {
      console.log(state.selected);
      let data = GetData.value
      var selectedCountry;
      // console.log(data.Countries);
      if (state.selected == 'Global' || state.selected == null) {
        console.log(state.selected);
        selectedCountry = data.Global
      }else {
        selectedCountry = data.Countries.find(country => country.Country == state.selected);
      }
      // console.log(selectedCountry)
      emit('selected-country', selectedCountry)
    }

    return {
      GetData,
      PassSelectedCountry,
      state
    }
  }
}
</script>

<style scoped lang="scss">
* {
  background: hsl(300, 100%, 25%);
}
.container {
  // width: 100vw;
  height: 6em;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 4em;
  // padding: 2em;
  @media (max-width: 768px){
    flex-direction: column;
    height: 8em;
    // padding: 2em 2em 2em 2em;
  }
  .title {
    font-size: 2em;
    margin-right: 1.2em;
  }
  .select {
    display: block;
    font-size: 1.5em;
    font-family: sans-serif;
    font-weight: 700;
    color: rgb(251, 251, 251);
    line-height: 1.3;
    padding: .6em 1.4em .5em .8em;
    width: 60%;
    box-sizing: border-box;
    margin: 0;
    border: 1px solid #aaa;
    box-shadow: 0 1px 0 1px rgba(0,0,0,.04);
    border-radius: .5em;
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    background-color: hsl(300, 100%, 23%);
    @media (max-width: 768px){
      width: 90%;
    }
  }
}
</style>