<template>
  <b-container fluid>
    <b-row> </b-row>
  </b-container>
</template>

<script>
// Imports
import axios from "axios";

export default {
  name: 'PhotoGrid',
  props: {
    msg: String
  },
  data(){
    return{
      apiElements:[],
    }
  },
  methods: {
    getImages(){
      const APIURL='https://jsonplaceholder.typicode.com/photos'
      axios.get(APIURL)
      .then(res => {
        console.log(res)
        this.apiElements=res
      })
      .catch(err => {
        console.error(err);
      })
    },
  },

  // -----Life cycle things------
  created(){

    this.getImages();
    
  },
  // -----END Life cycle things------
}
</script>

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
</style>
