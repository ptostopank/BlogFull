<template>
  <div id="SignIn">
    <form @submit="login">
      {{ form }}
      <div>
        <label for="Username"> Username </label>

        <input
          type="text"
          name="username"
          id="username_for_signin"
          v-model="form.username"
        />
      </div>
      <div>
        <label for="password1"> Password </label>

        <input
          type="password"
          name="password"
          id="password_for_signin"
          v-model="form.password"
        />
      </div>
      <div>
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignIn",
  components: {},
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    login(event) {
      event.preventDefault();

      this.axios
        .post("http://localhost:8000/api/auth/token/", {
          username: this.username,
          password: this.password,
        })
        .then((response) => {
          this.setLogined(response.data.token);
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>

<style>
#SignIn {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  width: 400px;
}
</style>
