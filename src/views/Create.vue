<template>
  <div>
    <v-container>
      <v-btn @click="addToFirestore">Save To Firestore</v-btn>
      <div>
        <h1 v-if="!this.madlib">Create Madlib</h1>
        <h1 v-else>Create New Madlib</h1>
      </div>
      <div>
        <v-btn v-if="!this.madlib" @click="getTemplate">Get template</v-btn>
        <v-btn v-else @click="getTemplate">Get New template</v-btn>
      </div>
    </v-container>
    <div v-if="!this.madlib">
      <v-container v-if="this.prompts">
        <v-form @submit.prevent="putMadlibTogether">
          <v-text-field
            v-for="(blanks, index) in prompts.blanks"
            :key="index"
            :placeholder="blanks"
            v-model="prompts.inputs[index]"
            outlined
          ></v-text-field>
          <v-btn v-if="prompts.blanks" type="submit">Create Madlib</v-btn>
        </v-form>
      </v-container>
    </div>
    <v-container v-if="madlib">
      <p>
        {{ madlib }}
      </p>
    </v-container>
  </div>
</template>

<script>
import { db } from "../firebase";
export default {
  methods: {
    async getTemplate() {
      this.prompts = [];
      this.madlib = null;
      fetch("http://madlibz.herokuapp.com/api/random?minlength=5&maxlength=10")
        .then((res) => res.json())
        .then((data) => {
          this.prompts = data;
          this.prompts.inputs = [];
        });
    },
    async putMadlibTogether() {
      const madlib = await this.prompts.value.map((e, i) => {
        return e + this.prompts.inputs[i];
      });
      this.madlib = await madlib.join(" ");
    },
    async addToFirestore() {
      console.log("ready to send");
      await db.collection("firstOne").add({
        data1: "test1",
        data2: "test2",
      });
      console.log("ran");
    },
  },
  data() {
    return {
      prompts: null,
      madlib: null,
    };
  },
};
</script>

<style></style>
