<template>
  <section class="container">
    <section class="title"><p class="titleName" style="">{{GetData.Country}} Cases</p></section>
    <section class="DataContainer">
      <section class="DepictedData">
        <section class="DepictedGrid">
          <p class="statsTitle">New Confirmed:</p>
          <img class="statsImage" src="../assets/icons/virus.svg">
          <p class="statsTitle">{{GetData.NewConfirmed}}</p>
        </section>
        <section class="DepictedGrid">
          <p class="statsTitle">Total Confirmed:</p>
          <img class="statsImage" src="../assets/icons/virus2.svg">
          <p class="statsTitle">{{GetData.TotalConfirmed}}</p>
        </section>
        <section class="DepictedGrid">
          <p class="statsTitle">New Deaths:</p>
          <img class="statsImage" src="../assets/icons/death3.svg">
          <p class="statsTitle">{{GetData.NewDeaths}}</p>
        </section>
        <section class="DepictedGrid">
          <p class="statsTitle">Total Deaths:</p>
          <img class="statsImage" src="../assets/icons/death2.svg">
          <p class="statsTitle">{{GetData.TotalDeaths}}</p>
        </section>
        <section class="DepictedGrid Mid">
          <p class="statsTitle">New Recovered:</p>
          <img class="statsImage" src="../assets/icons/recovered.svg">
          <p class="statsTitle">{{GetData.NewRecovered}}</p>
        </section>  
        <section class="DepictedGrid MidLeft">
          <p class="statsTitle">Total Recovered:</p>
          <img class="statsImage" src="../assets/icons/recover.svg">
          <p class="statsTitle">{{GetData.TotalRecovered}}</p>
        </section>             
      </section>
      <Chart :pieData="state.pieObject"/>
    </section>
  </section>
</template>

<script>
import {computed, reactive} from "vue";
import Chart from './Chart.vue';

export default {
  components: { Chart },
  name: "CovidCases",
  props: {
    GotData: {
      requiered: true
    },
    Test: {
      type: String,
      default: 'ssss'
    }
  },
  setup(props) {

    const state = reactive({

      pieObject: {},

      properitesToShow: [
        {name: 'NewConfirmed', imgSrc: require('../assets/icons/virus.svg')},
        {name: 'TotalConfirmed', imgSrc: require('../assets/icons/virus2.svg')},
        {name: 'NewDeaths', imgSrc: require('../assets/icons/death3.svg')},
        {name: 'NewRecovered', imgSrc: require('../assets/icons/death2.svg')},
        {name: 'TotalRecovered', imgSrc: require('../assets/icons/recover.svg')}
        ]
    })


    const GetData = computed(() => {
      console.log(props.GotData, 'from getData');
      CountPercentages(props.GotData)
      console.log(CountPercentages(props.GotData));
      return props.GotData
    })

  
    const CountPercentages = ((data)=> {
      let dataSummary;
      dataSummary = (parseInt(data.TotalConfirmed) + parseInt(data.TotalDeaths) + parseInt(data.TotalRecovered));
      var TCPerce;
      var TDPerce;
      var TRPerce;
      TCPerce = Math.round(data.TotalConfirmed / dataSummary * 100);
      TDPerce = Math.round(data.TotalDeaths / dataSummary * 100);
      TRPerce = Math.round(data.TotalRecovered / dataSummary * 100);
      console.log(TCPerce, TDPerce, TRPerce);
       state.pieObject = [
        {color: '#7FFF00', per: TCPerce},
        {color: '#00008B', per: TDPerce},
        {color: '#00BFFF', per: TRPerce}
      ]
    })

    return {
      state,
      GetData,
    }
  }
}
</script>

<style scoped lang="scss">
.container {
  color: #e3e5e5;
  margin-top: 3rem;
  
  // flex-direction: column;
  // width: 100vw;
  // height: 100vh;
  .title {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 2rem;
    // flex-direction: row;
    font-size: 3em;
    // background: #0de4e4;
    @media (max-width: 768px) {
      font-size: 2em;
      margin-bottom: 2em;
    }
    .titleName {
      border-bottom: solid 2px #e3e5e5
    }
  }
  .DataContainer {
    display: flex;
    align-items: center;
    justify-content: center;
    // margin: auto;
    // background: #da1959;
    flex-direction: column;
    width: 100%;
    min-height: 70vh;
    margin: auto;
    .DepictedData {
      // background: #3fe40d;
      display: grid;
      justify-content: center;
      grid-template-columns: repeat(4, auto);
      grid-template-rows: auto;
      grid-gap: 4rem;
      .DepictedGrid {
        text-align: center;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        .statsImage {
          align-self: center;
          width: 7vw;
          @media (max-width: 768px) {
            width: 20vw;
          }
        }
        .statsTitle {
          font-size: 2em;
        }
      }
      .Mid {
        grid-column: 3/2;
        @media (max-width: 768px) {
          grid-column: auto;;
        }
        // @media (max-width: 1024px) {
        //   grid-column: auto;;
        // }
      }
      
      @media (max-width: 768px) {
          grid-template-columns: repeat(1, 1fr);
        }
      // @media only screen 
      //     and (min-device-width: 768px) 
      //     and (max-device-width: 1024px) {
      //       padding: 4em;
      //       grid-template-columns: repeat(3, 1fr);
      //     } 
    }
  }
}
</style>