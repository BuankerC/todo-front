<template>
  <div>
    <div v-if="loading" class="spinner-border" role="status">
      <span class="sr-only">Loading...</span>
    </div>

    <div v-else class="login-div col-6 offset-3">
      <div class="form-group">
        <label for="id">ID</label>
        <input
          id="id"
          class="form-control"
          type="text"
          v-model="credential.username"
        />
      </div>
      <div class="form-group">
        <label for="password">PASSWORD</label>
        <input
          id="password"
          class="form-control"
          type="password"
          v-model="credential.password"
        />
      </div>
      <button class="btn btn-primary" @click="login">로그인</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      credential: {
        username: "",
        password: ""
      },
      loading: false
    };
  },
  methods: {
    login() {
      console.log("로그인 시도!!!");
      axios
        .post("http://localhost:8000/api-token-auth/", this.credential)
        .then(res => {
          this.loading = true;
          console.log(res);
        })
        .catch(e => {
          this.loading = true;
          console.log(e);
        });
    }
  }
};
</script>

<style></style>
