<template>
  <div>
    <h1>LOGIN</h1>
    <form @submit="login">
      <input v-model="username" placeholder="username" />
      <br />
      <br />
      <input v-model="password" placeholder="password" type="password" />
      <br />
      <br />
    <!-- {{setTes(tes)}} -->
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script>
import { mapMutations, } from "vuex";

export default {
  data: () => {
    return {
      username: "",
      password: "",
    };
  },
  // store:store,
  methods: {
    ...mapMutations(["setUser", "setToken"]),
    async login(e) {
      e.preventDefault();
      const response = await fetch("http://localhost:3000/login", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          username: this.username,
          password: this.password,
        }),
      });
      // console.log(response);
      
      if(response.status == 200) {
        console.log('dapet status 200');
        localStorage.setItem('username', this.username)
        localStorage.setItem('password', this.password)
      }
      // ------------------------
      
      // ------------------------

      // get token from response
      const { user, token } = await response.json();
      this.setUser(user);
      this.setToken(token);
      this.$router.push("/");
      // console.log('ini response', response);
      console.log('user', user);
      // console.log('ini token', token);
    },
  },
};
</script>

<style></style>
