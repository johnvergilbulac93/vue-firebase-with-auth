<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col s12 m8 offset-m2">
          <div
            class="login card-panel grey lighten-4 grey-text-darken-2 center"
          >
            <h3>Register</h3>
            <form @submit.prevent="register">
              <div class="input-field">
                <i class="material-icons prefix">email</i>
                <input type="text" id="email" tabindex="1" v-model="email" />
                <label for="email">Email</label>
              </div>
              <div class="input-field">
                <i class="material-icons prefix">lock</i>
                <input
                  type="password"
                  id="password"
                  tabindex="2"
                  v-model="password"
                />
                <label for="passsword">Password</label>
              </div>
              <button type="submit" class="btn btn-large teal white-text">
                Register
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
  name: "Register",
  data() {
    return {
      email: null,
      password: null
    };
  },
  methods: {
    register() {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(
          () => {
            alert(`Account created for ${this.email}`);
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
