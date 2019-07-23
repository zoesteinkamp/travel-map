<template>
  <div id="main">
    <div v-if="state === 'select'">
    <h3>Please Choose where you are from/living</h3>
    <select v-model="selectedCountryCost">
      <option v-for="option in countryOptions" v-bind:value="option.cost">
        {{ option.text }}
      </option>
    </select>
    <h3>Please Choose what kind of travel you are hoping to do</h3>
    <select v-model="selectedPrice">
      <option v-for="option in travelOptions" v-bind:value="option.id">
        {{ option.text }}
      </option>
    </select>
    <div id="buttonSpacing" v-if="selectedPrice != '' && selectedCountryCost != ''">
    <b-button variant="outline-primary" @click="searchList">Search</b-button>
    </div>
    </div>


    <div v-if="state === 'view'">
    <h1> Countries that match your criteria</h1>
      <li v-for="country in list">
        <b-card no-body class="overflow-hidden" style="max-width: 540px;">
          <b-row no-gutters>
            <b-col md="6">
              <b-card-img :src="country.image" class="rounded-0"></b-card-img>
            </b-col>
            <b-col md="6">
              <b-card-body>
              <b-card-title>{{country.text}}</b-card-title>
                <b-card-text>
                  Description to be added soon
                </b-card-text>
              </b-card-body>
            </b-col>
          </b-row>
        </b-card>
      </b-card>
      </li>
      <div id="buttonSpacing">
      <button class="btn btn-primary" @click="reset" > Reset </button>
      </div>
    </div>

    <div  v-if="state === 'expensivewarning'">
      <h1> Your Cost of living is so High there are no place too expensive for you to visit. </h1>
      <div id="buttonSpacing">
      <button class="btn btn-primary" @click="reset" > Return </button>
      </div>
    </div>

    <div  v-if="state === 'affordablewarning'">
    <h1> Your Cost of living is so low there are no affordable places for you to visit. </h1>
    <div id="buttonSpacing">
    <button class="btn btn-primary" @click="reset" > Return </button>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  data () {
     return{
       selectedCountryCost: '',
       selectedPrice: '',
       state: 'select',
       travelOptions : [
          { text: 'Affordable for me', id: 1 },
          { text: 'Similar cost as home', id: 2 },
          { text: 'Expensive for me', id: 3 }
       ],
       countryOptions: [
          { text: 'America', id: '1', cost: 5, image: require('../assets/America.jpg') },
          { text: 'Japan', id: '2', cost:5, image: require('../assets/japan.jpg') },
          { text: 'Thailand', id: '3', cost:3, image: require('../assets/Thailand.jpg') },
          { text: 'Nepal', id: '4', cost:1, image: require('../assets/nepal.jpg') },
          { text: 'Vietnam', id: '5', cost:2, image: require('../assets/vietnam.jpg') },
          { text: 'Taiwan', id: '6', cost:4, image: require('../assets/taiwan.jpg') },
          { text: 'China', id: '7', cost:4, image: require('../assets/china.jpg') },
          { text: 'Singapore', id: '8', cost:5, image: require('../assets/singapore.jpg') },
          { text: 'Australia', id: '9', cost:5, image: require('../assets/Australia.jpg') },
          { text: 'Brazil', id: '10', cost:4, image: require('../assets/brazil.jpg') },
          { text: 'Argentina', id: '11', cost:4, image: require('../assets/argentina.jpg') },
          { text: 'Costa Rica', id: '12', cost:3, image: require('../assets/costarica.jpg') },
          { text: 'France', id: '13', cost:5, image: require('../assets/france.jpg') },
          { text: 'Eritrea', id: '14', cost:1, image: require('../assets/eritrea.jpg') },
          { text: 'Croatia', id: '15', cost:4, image: require('../assets/croatia.jpg') },
          { text: 'Greece', id: '16', cost:4, image: require('../assets/greece.jpg') },
          { text: 'Turkey', id: '17', cost:4, image: require('../assets/turkey.jpg') },
          { text: 'Mauritania', id: '18', cost:2, image: require('../assets/mauritania.jpg') },
          { text: 'Mexico', id: '19', cost:3, image: require('../assets/mexico.jpg') },
          { text: 'Peru', id: '20', cost:3, image: require('../assets/peru.jpg') },
          { text: 'Norway', id: '21', cost:5, image: require('../assets/norway.jpg') },
          { text: 'Germany', id: '22', cost:5, image: require('../assets/germany.jpg') }
        ],
        list: [  ]
      }
   },
   // Corner cases and issues
   // 1. The same country will appear in the comforts of home list
   // 2. If you have a cost of 1, nothing will be in the affordable list
   methods: {
      searchList: function() {
          this.state = 'view'
          if(this.selectedPrice === 1){
          if(this.selectedCountryCost != 1){
          this.countryOptions.forEach((country) => {
            if(country.cost <  this.selectedCountryCost){
              this.list.push(country)
              }
          })
          }else{
          this.state = "affordablewarning";
          }
          }else if(this.selectedPrice === 2){
          this.countryOptions.forEach((country) => {
            if(country.cost === this.selectedCountryCost){
              this.list.push(country)
              }
          })
        }else{
          if(this.selectedCountryCost != 5){
          this.countryOptions.forEach((country) => {
            if(country.cost > this.selectedCountryCost){
              this.list.push(country)
              }
          })
          }else{
          this.state = "expensivewarning";
          }
        }
      },
      reset: function(){
        this.state = 'select';
        this.selectedPrice = '';
        this.selectedCountryCost = '';
        this.list = [];
      }
   }
}

</script>
<!-- Cost is 5 high, 4 hight middle, 3 middle, 2 low middle, 1 poor -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#main{
  margin: 20px 20px 10px 10px;
  text-align: center;

}

#buttonSpacing{
margin: 10px 0 0 0;
}
</style>
