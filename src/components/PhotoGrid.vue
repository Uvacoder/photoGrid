<template>
  <b-container fluid>
    <b-row
      cols="1"
      cols-sm="2"
      cols-md="4"
      cols-lg="6"
      cols-xl="8"
      align-v="center"
      align-h="center"
    >
      <b-jumbotron
        v-for="item in showElements"
        :key="item.id"
        class="m-2"
        border-variant="grey"
        fluid
      >
        <b-col>
          <b-row>
            <b-col>
              <div class="h6">{{ item.title }}</div>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <b-img :src="item.thumbnailUrl"></b-img>
            </b-col>
          </b-row>
        </b-col>
      </b-jumbotron>
    </b-row>
  </b-container>
</template>

<script>
// Imports
import axios from "axios";
// import { Row, Column } from 'vue-grid-responsive';

export default {
  name: "PhotoGrid",
  props: {
    msg: String,
  },
  data() {
    return {
      apiElements: [],
      showElements: [],
      albumSelected: 1,
    };
  },
  methods: {
    getImages() {
      const APIURL = "https://jsonplaceholder.typicode.com/photos";
      axios
        .get(APIURL)
        .then((res) => {
          this.apiElements = res.data;
          this.apiElements.filter((item) => {
            if (item.albumId == 1) {
              this.showElements.push(item);
            }
          });
        })
        .catch((err) => {
          console.error(err);
        });
    },
    getNextAlbum() {
      window.onscroll = () => {
        let bottomOfWindow =
          document.documentElement.scrollTop + window.innerHeight ===
          document.documentElement.offsetHeight;

        if (bottomOfWindow) {
          this.albumSelected++;
          this.apiElements.filter((item) => {
            if (item.albumId == this.albumSelected) {
              this.showElements.push(item);
            }
          });
          console.log(this.albumSelected);
            
        }
      };
    },
  },

  // -----Life cycle things------
  created() {},
  beforeMount() {
    this.getImages();
  },
  mounted() {
    this.getNextAlbum();
    console.log("this.showElements------", this.showElements);
  },
  // -----END Life cycle things------
};
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
