<template>
  <div>
    <v-container>
      <h1>Create Madlib</h1>
      <v-btn @click="getTemplate">Get template</v-btn>
    </v-container>
    <v-container v-if="this.prompts">
      <v-form @submit.prevent="saveInputs">
        <v-text-field
          v-for="(blanks, index) in prompts.blanks"
          :key="index"
          :placeholder="blanks"
          v-model="prompts.inputs[index]"
          outlined
        ></v-text-field>
        <v-btn type="submit">Save Answers</v-btn>
      </v-form>
    </v-container>
  </div>
</template>

<script>
import { db } from "../firebase";

export default {
  methods: {
    async getTemplate() {
      this.prompts = [];
      fetch("http://madlibz.herokuapp.com/api/random")
        .then((res) => res.json())
        .then((data) => {
          this.prompts = data;
          this.prompts.inputs = [];
        });
    },
    async saveInputs() {
      await db.collection("userInputs").add({
        data1: "test1",
        data2: "test2",
      });
    },
  },
  data() {
    return {
      prompts: null,
    };
  },
};
</script>

<style></style>
