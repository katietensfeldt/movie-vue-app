<template>
  <div class="actors-show">
    <div class="card mb-3">
      <img :src="actor.image" class="card-img-top" alt="actor image" />
      <div class="card-body">
        <h5 class="card-title">{{ actor.full_name }}</h5>
        <p class="card-text">{{ actor.full_name }} is {{ actor.age }}.</p>
        <p class="card-text">They are most known for {{ actor.known_for }}, as well as {{ actor.movie.title }}</p>
        <div class="btn-group" role="group" aria-label="Basic mixed styles example">
          <router-link :to="`/actors/${actor.id}/edit`" class="btn btn-warning">Edit</router-link>
          <button v-on:click="destroyActor()" type="button" class="btn btn-danger">Delete</button>
        </div>
      </div>
    </div>
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
