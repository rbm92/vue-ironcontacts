<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <!-- <img :src="contact.pictureUrl"> -->
    <h1>IronContacts</h1>
    <div><button @click="addContact">Add Random Contact</button></div>
    <div class="header">
      <h2>Picture</h2>
      <h2>Name</h2>
      <h2>Popularity</h2>
      <h2>Won Oscar</h2>
      <h2>Won Emmy</h2>
    </div>
    <div class="contact" v-for="contact in initialList">
      <img :src="contact.pictureUrl" :alt="contact.name" width="50" />
      <div>{{ contact.name }}</div>
      <div>{{ contact.popularity.toFixed(2) }}</div>
      <div v-if="contact.wonOscar">🏆</div>
      <div v-else></div>
      <div v-if="contact.wonEmmy">🏆</div>
      <div v-else></div>
    </div>
    <!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
  </div>
</template>

<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
import contacts from "./contacts.json";

const myContacts = contacts;
let initialList = myContacts.slice(0, 5);
let remaining = myContacts.slice(5);
// console.log(initialList);
// console.log(remaining);

function addContact() {
  let randomNum = Math.floor(Math.random() * remaining.length);
  // console.log(randomNum);
  console.log(remaining[randomNum]);
  const newList = initialList.push(remaining[randomNum]);
  initialList = newList;
  
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
.header,
.contact {
  display: flex;
  gap: 30px;
  margin: 10px;
  align-items: center;
  justify-content: center;
}

.contact img,
.contact div,
.header h2 {
  width: 100px;
}
</style>
