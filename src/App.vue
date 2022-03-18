<template>
  <div>
    <img width="100" alt="Vue logo" src="./assets/logo.png" />
    <!-- <img :src="contact.pictureUrl"> -->
    <h1>IronContacts</h1>
    <div class="buttons">
      <button @click="addContact">Add Random Contact</button>
      <button @click="sortPopularity">Sort By Popularity</button>
      <button @click="sortName">Sort By Name</button>
    </div>
    <div class="header">
      <h2>Picture</h2>
      <h2>Name</h2>
      <h2>Popularity</h2>
      <h2>Won Oscar</h2>
      <h2>Won Emmy</h2>
      <h2>Actions</h2>
    </div>
    <div class="contact" v-for="contact in initialList">
      <img :src="contact.pictureUrl" :alt="contact.name" width="50" />
      <div>{{ contact.name }}</div>
      <div>{{ contact.popularity.toFixed(2) }}</div>
      <div v-if="contact.wonOscar">🏆</div>
      <div v-else></div>
      <div v-if="contact.wonEmmy">🏆</div>
      <div v-else></div>
      <div>
        <button @click="deleteContact(contact)">Delete</button>
      </div>
    </div>
    <!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
  </div>
</template>

<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
import contacts from "./contacts.json";
import { ref, reactive, computed } from "vue";

const myContacts = reactive(contacts);
const initialList = reactive(contacts.slice(0, 5)); // initially 5
const remaining = reactive(contacts.slice(5)); // the remaning 47

function addContact() {
  const randomNum = Math.floor(Math.random() * remaining.length);
  // pick a random actor from the remaining list

  initialList.push(remaining[randomNum]); // add actor to the initial list
  remaining.splice(randomNum, 1); // remove actor from the remaining list
}

function sortPopularity() {
  initialList.sort((a, b) => (a.popularity < b.popularity ? 1 : -1));
}

function sortName() {
  initialList.sort((a, b) => (a.name > b.name ? 1 : -1));
}

function deleteContact(contact) {
  const index = initialList.indexOf(contact);
  initialList.splice(index, 1);
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
.contact, .buttons {
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