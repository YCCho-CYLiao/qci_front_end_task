<template>
  <div class="search">
   
 
   <h2> Select the Date </h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type = "date" v-model="query" />
     <p><button>Submit</button></p>
    </form>
    

    <div class="results" v-if="results">
      <div v-for="result in results" v-bind:key="result">
          <h3> Camera: {{result.camera.name}}, Rover: {{result.rover.name}}</h3>
          <p> Landing_date: {{result.rover.landing_date}}.  Launch_date: {{result.rover.launch_date}}.</p>
          <img v-bind:src="result.img_src" />

      </div>
    </div>

  </div>


</template>

<script>
import axios from 'axios';

//const KEY = uXDlMtOsbU9bO622lPG3UGoyw9OjiSOfMEzl6YFa;
export default {
  name: 'search',

  data() {
    return{
          query: '',
          value: '',
          results: '',
          date: null
    }
  },
  methods:{
    getResult(query){
       
       axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/Curiosity/photos?api_key=uXDlMtOsbU9bO622lPG3UGoyw9OjiSOfMEzl6YFa&earth_date=' + query).then (response => {
        console.log(response.data.photos);
        //console.log(query);

        this.results = response.data.photos;
       });
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.results img{
  height: 300px;
  margin: 10px;
}
h3 {
  margin: 5px 0 0;
  color: #4254b9;
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
</style>
