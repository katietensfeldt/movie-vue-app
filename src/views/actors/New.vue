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
        <label>
          First Name:
          <input type="text" required class="form-control" v-model="newActorParams.first_name" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Last Name:
          <input type="text" required class="form-control" v-model="newActorParams.last_name" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Known For:
          <input type="text" class="form-control" v-model="newActorParams.known_for" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Gender:
          <select>
            <option value="M">Male</option>
            <option value="F">Female</option>
            <option value="O">Other</option>
          </select>
        </label>
      </div>
      <div class="form-group">
        <label>
          Age:
          <input type="number" class="form-control" v-model="newActorParams.age" />
        </label>
      </div>
      <div class="form-group">
        <label>
          Movie Id:
          <input type="text" class="form-control" v-model="newActorParams.movie_id" />
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
