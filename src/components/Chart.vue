<template>
  <p class="title">Data Depicted in charts:</p>
  <div class="PieChart" :style="PieStyles"></div>
  <section class="ChartDescribtion">
    <div class="name">
      <div class="color" style="background: #7FFF00"></div>
      Total Confirmed: {{getData[0].per}}%
    </div>      
    <div class="name">
      <div class="color" style="background: #00BFFF"></div>
      Total recovered: {{getData[2].per}}% 
    </div>
    <div class="name">
      <div class="color" style="background: #00008B"></div>
      Total Deaths: {{getData[1].per}}%
    </div>
  </section>
</template>

<script>
import { computed, reactive } from 'vue'

export default {
  props: {
    pieData: {
      requiered: true,
    }
  },
  setup(props) {

    const state = reactive({
      dataToDepict: []
    })

    const getData = computed(() => {
      return props.pieData
    })

    const PieStyles = computed(()=> {
      let sum = 0;
      let styles = props.pieData.map(
        piePart => `${piePart.color} 0 ${sum += piePart.per}%`
      ) 
      return {background: 'conic-gradient(' + styles.join(",") + ')'};
    })

    return {
      PieStyles,
      state,
      getData
    }
  }

}
</script>

<style lang="scss" scoped>
.PieChart {
  width: 30vw;
  height: 30vw;
  border-radius: 50%;
  @media (max-width: 768px) {
    width: 70vw;
    height: 70vw;
  }  
}
.title {
  text-align: center;
  font-size: 3em;
  margin: 2rem;
  border-bottom: solid 2px #e3e5e5;
  @media (max-width: 768px) {
    font-size: 2em;
  }
}
.ChartDescribtion {
  margin-top: 2rem;
  margin-bottom: 2rem;
  // display: grid;
  grid-template-columns: 3 1fr;
  .name {
  font-size: 2em;
  display: flex;
  @media (max-width: 768px) {
    font-size: 1.5em;
  }
  .color {
    margin-right: 1rem;
    width: 1em;
    height: 1em;
    // background: #e3e5e5;
    
  }
}
}

</style>