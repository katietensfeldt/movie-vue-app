<template>
  <div class="actors-edit">
    <form v-on:submit.prevent="editActor()">
      <h1>Edit Actor</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>First Name:</label>
        <input type="text" class="form-control" v-model="editActorParams.first_name" />
      </div>
      <div class="form-group">
        <label>Last Name:</label>
        <input type="text" class="form-control" v-model="editActorParams.last_name" />
      </div>
      <div class="form-group">
        <label>Known For:</label>
        <input type="text" class="form-control" v-model="editActorParams.known_for" />
      </div>
      <div class="form-group">
        <label>Gender:</label>
        <input type="text" class="form-control" v-model="editActorParams.gender" />
      </div>
      <div class="form-group">
        <label>Age:</label>
        <input type="text" class="form-control" v-model="editActorParams.age" placeholder="True or false" />
      </div>
      <div class="form-group">
        <label>Movie Id:</label>
        <input type="text" class="form-control" v-model="editActorParams.movie_id" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    editActorParams: {},
    errors: [],
  }),
  created: function () {
    axios.get(`/actors/${this.$route.params.id}`).then((response) => {
      this.editActorParams = response.data;
      console.log(response.data);
    });
  },
  methods: {
    editActor: function () {
      axios
        .patch(`/actors/${this.editActorParams.id}`, this.editActorParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/actors/${response.data.id}`);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
