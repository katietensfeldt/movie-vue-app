<template>
  <div class="actors-new">
    <form v-on:submit.prevent="createActor()">
      <h1>Add New Actor</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>First Name:</label>
        <input type="text" class="form-control" v-model="newActorParams.first_name" />
      </div>
      <div class="form-group">
        <label>Last Name:</label>
        <input type="text" class="form-control" v-model="newActorParams.last_name" />
      </div>
      <div class="form-group">
        <label>Known For:</label>
        <input type="text" class="form-control" v-model="newActorParams.known_for" />
      </div>
      <div class="form-group">
        <label>Gender:</label>
        <input type="text" class="form-control" v-model="newActorParams.gender" />
      </div>
      <div class="form-group">
        <label>Age:</label>
        <input type="text" class="form-control" v-model="newActorParams.age" placeholder="True or false" />
      </div>
      <div class="form-group">
        <label>Movie Id:</label>
        <input type="text" class="form-control" v-model="newActorParams.movie_id" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    newActorParams: {},
    errors: [],
  }),
  methods: {
    createActor: function () {
      axios
        .post("/actors", this.newActorParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/actors");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
