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
        <label>
          First Name:
          <input type="text" class="form-control" v-model="editActorParams.first_name" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Last Name:
          <input type="text" class="form-control" v-model="editActorParams.last_name" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Image URL:
          <input type="text" class="form-control" v-model="editActorParams.image" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Known For:
          <input type="text" class="form-control" v-model="editActorParams.known_for" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Gender:
          <input type="text" class="form-control" v-model="editActorParams.gender" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Age:
          <input type="text" class="form-control" v-model="editActorParams.age" placeholder="True or false" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Movie Id:
          <input type="text" class="form-control" v-model="editActorParams.movie_id" />
        </label>
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
