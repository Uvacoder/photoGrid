<template>
  <b-container class="containerEdit" fluid>
    <b-row
      cols="1"
      cols-sm="3"
      cols-md="4"
      cols-lg="6"
      cols-xl="8"
      align-v="center"
      align-h="center"
    >
      <Item-grid
        v-for="item in showElements"
        :dataItem="item"
        :key="item.id"
        @delete="onDeleteItem"
      />
    </b-row>
  </b-container>
</template>

<script>
// Imports
import axios from "axios";
import ItemGrid from "./ItemGrid.vue";
import "animate.css";

export default {
  name: "PhotoGrid",
  components: {
    ItemGrid,
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
          if (this.albumSelected < 100) {
            this.albumSelected++;
          }
          this.apiElements.filter((item) => {
            if (item.albumId == this.albumSelected) {
              this.showElements.push(item);
            }
          });
        }
      };
    },
    onDeleteItem(id) {
      this.showElements = this.showElements.filter((ele) => ele.id != id);
    },
  },

  // -----Life cycle things------
  created() {},
  beforeMount() {
    this.getImages();
  },
  mounted() {
    this.getNextAlbum();
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

.containerEdit {
  background-color: #8a89892d;
}
</style>
