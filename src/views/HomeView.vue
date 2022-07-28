<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      contacts: [],
    };
  },
  created: function () {
    this.indexContacts();
  },
  methods: {
    indexContacts: function () {
      axios.get("/contacts").then((response) => {
        this.contacts = response.data;
        console.log(response.data);
      });
    },
    createContact: function () {
      console.log("New Contact Created!");
      var params = {
        name: this.newContactName,
        phone: this.newPhone,
        email: this.newEmail,
        birthday: this.newBirthday,
        address: this.newAddress,
      };
      // console.log(params);
      axios.post("/contacts", params).then((response) => {
        console.log("Great Success!", response.data);
        this.contacts.push(response.data);
        this.newContactName = "";
        this.newPhone = "";
        this.newEmail = "";
        this.newBirthday = "";
        this.newAddress = "";
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>New Contact</h1>
    Name:
    <input type="text" v-model="newContactName" />
    Phone:
    <input type="text" v-model="newContactPhone" />
    Email:
    <input type="text" v-model="newContactEmail" />
    Birthday:
    <input type="text" v-model="newContactBirthday" />
    Address:
    <input type="text" v-model="newContactAddress" />
    <button v-on:click="createContact()">Create Contact</button>
    <h1>{{ message }}</h1>
    <div v-for="contact in contacts" v-bind:key="contact.id"></div>
  </div>
</template>

<style></style>
