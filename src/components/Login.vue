<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col s12 m8 offset-m2">
          <div
            class="login card-panel grey lighten-4 grey-text-darken-2 center"
          >
            <h3>Login</h3>
            <form @submit.prevent="login">
              <div class="input-field">
                <i class="material-icons prefix">email</i>
                <input type="text" id="email" tabindex="1" v-model="email" />
                <label for="email">Email</label>
              </div>
              <div class="input-field">
                <i class="material-icons prefix">lock</i>
                <input
                  type="password"
                  id="passwo"
                  tabindex="2"
                  v-model="password"
                />
                <label for="passsword">Password</label>
              </div>
              <button
                type="submit"
                class="btn btn-large teal white-text"
                tabindex="3"
              >
                Login
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/firebase-auth";
export default {
  name: "Login",
  data() {
    return {
      email: null,
      password: null
    };
  },
  methods: {
    login() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            alert(`You are logged in as ${user.user.email}`);
            this.$router.go({ path: this.$router.path });
          },
          err => {
            alert(err.message);
          }
        );
    }
  }
};
</script>

<style scoped></style>
