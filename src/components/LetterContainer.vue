<template>
  <div :class="letterClass">{{letter}}</div>
</template>

<style scoped>
div {
  float: left;
  font-size: 2em;
  margin: 0.25em;
  border: #2c3e50 solid;
  width: 30px;
  height: 50px;
  color: #fff;
}

div.correct {
  background-color: #538d4e;
}

div.contains {
  background-color: #b59f3b;
}
</style>

<script>
  export default {
    props: {
      letter: {
        required: true,
        type: String,
      },
      letterClass: {
        required: true,
        type: String,
      }
    },
  }
</script>