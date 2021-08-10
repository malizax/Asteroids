<template>
  <div class="home">
    <section class="hero is-dark">
      <div class="from_to_range">
        <label for="from">From:</label>
        <input v-model="from_message" type="text" id="from"/>
        <p>Message From is: {{ from_message }}</p>
        <label for="to">To:</label>
        <input v-model="to_message" type="text" id="to"/>
        <p>Message To is: {{ to_message }}</p>
        <input type="checkbox" id="checkbox" v-model="checked">
        <label for="checkbox"> {{ checked }}</label>
      </div>
      <div>
      {{ info }}
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios';

let fM = 'YYYY-mm-dd';
let readyFlag = false;
let forV = fM;
let toV = fM;
//const apiKey = 'CsjJjfAJnjB42lman0uI6INY5jEWemqR7wFA4s7y';


export default {
  name: 'home',
  components: {
  },
  data(){
      return {
          from_message: forV,
          to_message: toV,
          checked: readyFlag,
          info: null
          }
  },
  mounted() {
      if(readyFlag) {
          axios
          //.get('https://api.nasa.gov/neo/rest/v1/feed?start_date=' + forV +
          //'&end_date=' + toV + '&api_key=' + apiKey)
          .get('https://api.nasa.gov/neo/rest/v1/feed?start_date=2021-08-01&end_date=2021-08-08&api_key=CsjJjfAJnjB42lman0uI6INY5jEWemqR7wFA4s7y')
          .then(response => (this.info = response))
          }
      }
}
</script>
