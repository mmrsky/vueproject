<template>
  <div class="matkalasku">
    <!-- <h1>{{ msg }}</h1> -->
    <h1>Matkalaskutin</h1>
    <h4>Anna matkan alkupäivä</h4>
    <input type="text" name=""> <!-- value="" v-model="newItem" @keyup.enter="addToList()">-->
    <h4>Anna matkan loppuaika</h4>
    <input type="text" name=""> <!-- value="" v-model="newItem" @keyup.enter="addToList()">-->
    <h4>Anna matkan kohde</h4>
    <input type="text" name=""> <!-- value="" v-model="newItem" @keyup.enter="addToList()">-->    
    <h4>Anna matkan aihe</h4>
    <input type="text" name=""> <!-- value="" v-model="newItem" @keyup.enter="addToList()">-->    
    <br><button>Lähetä</button>
  </div>
</template>

<script>
export default {
  name: 'Matkalasku',
  props: {
    msg: String
  }
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
