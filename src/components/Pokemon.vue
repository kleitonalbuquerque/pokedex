<template>
  <div class="container">
    <h1>{{ num }} - {{ name | upper }}</h1>
    <small>{{ url }}</small>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      pokemon: {},
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  created: function () {
    axios.get(this.url).then((res) => {
      // console.log(res.data);
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      console.log(this.pokemon);
    });
  },
  filters: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
};
</script>

<style></style>
