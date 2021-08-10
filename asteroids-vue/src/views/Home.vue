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
        <input type="checkbox" id="checkbox" v-model="checked"
        @change="callNASA()">
        <label for="checkbox"> {{ checked }}</label>
      </div>
      <div>
      {{ info }}
      </div>
      <div v-if="errored">
        <p>REST call errored out?</p>
      </div>
      <div v-else>
        <div v-if="loading">Loading...</div>
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
const apiKey = 'CsjJjfAJnjB42lman0uI6INY5jEWemqR7wFA4s7y';

export default {
  name: 'home',
  components: {
  },
  data(){
      return {
          from_message: forV,
          to_message: toV,
          checked: readyFlag,
          info: null,
          loading: true,
          errored: false
          }
  },
  methods: {
      callNASA() {
          alert('call NASA is called with a from value of ' +
          this.from_message + ' and a to value of ' + this.to_message);
          if(this.checked) {
              axios
              .get('https://api.nasa.gov/neo/rest/v1/feed?', {
                  params: {
                      start_date: this.from_message,
                      end_date: this.to_message,
                      api_key: apiKey
                      }
                })
              .then(response => {
                  this.info = response
                })
              .catch(error => {
                  console.log(error)
                  this.errored = true
                })
              .finally(() => this.loading = false)
              }
        }
}
,
  computed: {
      /*
      axiosParams() {
          const params = new URLSearcParams();
          params.append('param1', this.from_message);
          params.append('param2', this.to_message);
          return params;
          }
          */
      },
  mounted() {
      //if(readyFlag) {
          //.get('https://api.nasa.gov/neo/rest/v1/feed?start_date=' + forV +
          //'&end_date=' + toV + '&api_key=' + apiKey)
          }
  }
</script>
