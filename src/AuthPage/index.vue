<template>
    <div class="login-page">
      <div class="card">
        <form @submit.prevent="login">
          <div class="title">Login</div>
          <input placeholder="Username" type="text" v-model="username" />
          <br />
          <input placeholder="Password" type="password" v-model="password" />
          <br />
          <button type="submit">Login</button>
        </form>
        <br>
        <form @submit.prevent="signup">
          <div class="title">Sign Up</div>
          <input
            class="input"
            placeholder="Username"
            type="text"
            v-model="username"
          />
          <br />
          <input placeholder="Password" type="password" v-model="password" />
          <br />
          <input placeholder="Email" type="text" v-model="email" />
          <br />
          <input placeholder="First name" type="text" v-model="first_name" />
          <br />
          <input placeholder="Last name" type="text" v-model="last_name" />
          <br />
          <button type="submit">Sign Up</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import { loginRest, signupRest } from "./api";
  
  export default {
    data() {
      return {
        username: "",
        password: "",
        email: "",
        first_name: "",
        last_name: "",
      };
    },
    methods: {
      login() {
        loginRest(this.username, this.password)
          .then((response) =>
            this.$emit("onAuth", { ...response.data, secret: this.password })
          )
          .catch((error) => console.log("Login error", error));
      },
      signup() {
        signupRest(
          this.username,
          this.password,
          this.email,
          this.first_name,
          this.last_name
        )
          .then((response) =>
            this.$emit("onAuth", { ...response.data, secret: this.password })
          )
          .catch((error) => console.log("Sign up error", error));
      },
    },
  };
  </script>
  
  <style>
  .login-page {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f5f5f5;
  }
  
  .card {
    padding: 24px;
    border-radius: 4px;
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
    background-color: #fff;
    width: 320px;
    text-align: center;
  }
  
  .title {
    font-size: 24px;
    margin-bottom: 16px;
    font-weight: bold;
  }
  
  input[type="text"],
  input[type="password"] {
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-bottom: 8px;
    width: 100%;
    box-sizing: border-box;
  }
  
  button[type="submit"] {
    background-color: #0077cc;
    color: #fff;
    padding: 8px 16px;
    border-radius: 4px;
    border: none;
    cursor: pointer;
    margin-top: 16px;
  }
  </style>
  