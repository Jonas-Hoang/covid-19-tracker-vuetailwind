<template>
  <main v-if="!loading">
    
      <DataTitle :text="title" :dataDate="dataDate"/>
      <DataBoxes :stats="stats"/>
      <CountrySelect @get-country="getCountryData" :countries="countries"/>
      <button @click="clearData" class=" content-center 
      text-center bg-green-700 text-white p-3 mx-5 mr-5 
      rounded-3xl focus:outline-none hover:bg-green-600O">
      Clear the country
      </button>
      
  </main>
  <main v-else class="">
      <div class="text-gray-500 text-3xl mt-10 mb-6 text-center">
        Fetching Data
      </div>
      <img :src="loadingImage" class="w-24 m-auto" alt="">
  </main>
</template>

<script>
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'


export default {
  name: 'HomeView',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data(){
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/giphy.gif')
    }
  },
  methods:{
    // Death error api methods
    async fetchCovidData(){
      const res = await fetch('https://covid-api.com/api/reports/total?date=2020-04-15')
      const data = await res.json()
      console.log(res)
      return data
    },
    getCountryData(country){
    this.stats = country;
    this.title = country.Country
    },
    async clearData(){
      this.loading = true;
      const data = await this.fetchCovidData();
      this.stats = data.Global;
      this.title = 'Global'
      this.loading = false
    },
  },
  
  async created(){
    const data= await this.fetchCovidData()
    console.log(data);
    console.log('alo9 alo9 ' + data.data.deaths);
    this.dataDate = data.data.date;
    this.stats = data.data;
    this.countries = data.data.Countries;
    this.loading = false
    
  },
}
</script>
