<template>
  <b-jumbotron
    class="m-2 jumboEdit rounded animate__animated animate__fadeIn"
    :class="classDelete"
    border-variant="grey"
    fluid
    @click="onClick"
  >
    <b-col>
      <b-row>
        <b-col>
          <div class="h6">{{ dataItem.title }}</div>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-img class="mb-2" :src="dataItem.thumbnailUrl"></b-img>
        </b-col>
      </b-row>
    </b-col>
  </b-jumbotron>
</template>

<script>
import "animate.css";

export default {
  name: "ItemGrid",
  props: {
    dataItem: {},
  },
  data() {
    return {
      classDelete: "",
    };
  },
  methods: {
    onClick() {
      this.classDelete = "animate__fadeOut";

      setTimeout(() => {
        this.$emit("delete", this.dataItem.id);
      }, 600);
    },
  },
};
</script>

<style>
.jumboEdit {
  min-width: 200px;
  background-color: #fff;
}
</style>