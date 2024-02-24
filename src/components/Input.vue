<template>
  <input type="number" placeholder="Input number" @input="changeAmount($event.target.value)" min="0"><br>
  <button @click="convert()">Convert</button>
  <button @click="favorite()" class="fav-button">Add to Favorites</button>
</template>

<script>
  export default {
    props: {
      changeAmount: {
        type: Function,
        required: true
      },
      convert: {
        type: Function,
        required: true
      },
      favorite:{
        type: Function,
        required: true
      }
    }
  }

</script>

<style scoped>
  input {
    border-radius: 3px;
    border: 0;
    width: 500px;
    font-size: 1.2em;
    padding: 10px 15px;
    background: #fafafa;
    outline: none;
    position: relative;
    top: -50px;
    color: #333;
  }

  button{
    color: #fff;
    position: relative;
    top: -20px;
    padding: 15px 20px;
    text-transform: uppercase;
    cursor: pointer;
    background: #28b685;
    border: 0;
    border-radius: 3px;

  }

  button.fav-button{
    margin-left: 20px;
  }
</style>