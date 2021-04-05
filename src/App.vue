<template>
  <img v-bind:class="gender" v-bind:src="image" alt="">
  <h1>{{firstName}} {{lastName}}</h1>
  <h4>{{email}}</h4>
  <button v-on:click="getrandom()">get random</button>
</template>

<script>
  export default {
    data () {
      return {
        firstName : "",
        lastName : "",
        email : "",
        image : "",
        gender : ""
      }
    },
    methods : {
      getrandom : async function() {
        let res = await fetch('https://randomuser.me/api')
        let data = await res.json();
        // console.log(data.results[0]);
        this.firstName = data.results[0].name.first;
        this.lastName = data.results[0].name.last;
        this.email = data.results[0].email;
        this.image = data.results[0].picture.large;
        this.gender = data.results[0].gender;
      }
    },
    beforeMount() {
      this.getrandom();
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.male {
  border: 5px solid rgb(190, 23, 23);
  border-radius: 20px;
}
.female {
  border: 5px solid rgb(165, 190, 23);
  border-radius: 20px;
}
</style>
