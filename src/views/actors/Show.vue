<template>
  <div class="actors-show">
    <h2>{{ actor.first_name }} {{ actor.last_name }}</h2>
    <p>Age: {{ actor.age }}</p>
    <p>Gender: {{ actor.gender }}</p>
    <p>Known For: {{ actor.known_for }}</p>
    <p>Also known for: {{ actor.movie.title }}, {{ actor.movie.year }}</p>
    <router-link :to="`/actors/${actor.id}/edit`">Edit</router-link>
    |
    <button v-on:click="destroyActor()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    actor: { movie: {} },
  }),
  created: function () {
    axios.get(`/actors/${this.$route.params.id}`).then((response) => {
      this.actor = response.data;
      console.log(response.data);
    });
  },
  methods: {
    destroyActor: function () {
      if (confirm("Are you sure you want to delete this actor?")) {
        axios.delete(`/actors/${this.actor.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/actors");
        });
        console.log("Destroyed!");
      }
    },
  },
};
</script>
