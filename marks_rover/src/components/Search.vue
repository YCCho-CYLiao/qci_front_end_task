<template>
  <div class="search">
    <h2> Type In Your Search Term </h2>
    <form v-on:submit.prevent="getResult(query)">
      <input type = "text" placeholder="Type in your search" v-model="query" />
    </form>
    <div class="results" v-if="results">
      <div v-for="result in results" v-bind:key="result">
       <!--<img v-bind:src="result.links[0].href" /> -->
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
          msg: 'Search',
          query: '',
          results: ''
    }
  },
  methods:{
    getResult(query){
       
       axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/opportunity/photos?api_key=uXDlMtOsbU9bO622lPG3UGoyw9OjiSOfMEzl6YFa&earth_date=' + query).then (response => {
        console.log(response);
        this.results = response.data.photos;
       });
      /*
        axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image').then (response => {
        console.log(response.data.collection.items);
        this.results = response.data.collection.items;
      }); */
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.results img{
  height: 300px;
  margin: 10px;
}
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
</style>
