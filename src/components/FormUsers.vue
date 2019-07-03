<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        USUARIOS
      </div>
      <div class="card-body">
        <form
          id="app"
          @submit="checkForm"
          action="https://vuejs.org/"
          method="post"
          >

          <p v-if="errors.length">
            <b>Please correct the following error(s):</b>
            <ul>
              <li v-for="(error, index) in errors" :key="index">{{ error }}</li>
            </ul>
          </p>

          <div class="form-group col-md-6">
            <label for="name">Name</label>
            <input
              id="name"
              v-model="name"
              type="text"
              name="name"
              class="form-control"
            >
          </div>

          <div class="form-row col-md-6">
            <div class="col-7">
              <input type="text" class="form-control" placeholder="City">
            </div>
            <div class="col">
              <input type="text" class="form-control" placeholder="State">
            </div>
            <div class="col">
              <input type="text" class="form-control" placeholder="Zip">
            </div>
          </div>

          <div class="form-group col-md-6">
            <label for="age">Age</label>
            <input
              id="age"
              v-model="age"
              type="number"
              name="age"
              min="0"
              class="form-control"
            >
          </div>

          <div class="form-group col-md-6">
            <label for="movie">Favorite Movie</label>
            <v-select name="movie" class="" v-model="movie" :options="options"></v-select>
          </div>

          <p>
            <input
              type="submit"
              value="Submit"
              class="btn btn-primary"
            >
          </p>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import vSelect from 'vue-select'
import 'vue-select/dist/vue-select.css';

export default {
  name: 'FormUsers',
  components:{
    vSelect
  },
  data(){
    return{
      errors: [],
      name: null,
      age: null,
      movie: null,
      options: [
        'Star Wars',
        'Vanilla Sky',
        'Atomic Blonde'
      ]
    }
  },
  methods:{
    checkForm: function (e) {

      if (this.name && this.age && this.movie) {
        return true;
      }

      this.errors = [];

      if (!this.name) {
        this.errors.push('Name required.');
      }
      if (!this.age) {
        this.errors.push('Age required.');
      }
      if (!this.movie) {
        this.errors.push('Movie required.');
      }
      
      e.preventDefault();
    }
  }
}
</script>
