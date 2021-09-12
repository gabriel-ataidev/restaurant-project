<template>
  <div class="items-list">
    {{ itemsList }}
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ItemsList",
  data() {
      return {
          itemsList: []
      }
  },
  created() {
    axios.get("http://localhost:3000/burguers").then((response) => {
      this.itemsList = response.data;
    });
  },
};
</script>

<style></style>
