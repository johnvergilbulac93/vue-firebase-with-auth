<template>
  <div id="navbar">
    <nav>
      <div class="nav-wrapper teal lighten-2">
        <div class="container">
          <router-link to="/" class="brand-logo">Employee Manager</router-link>
          <ul id="nav-mobile" class="right hide-on-md-and-down">
            <li v-if="isLoggedIn">
              <span class="email">{{ currentUser }}</span
              >&nbsp;
            </li>

            <li v-if="!isLoggedIn">
              <router-link to="/login">Login</router-link>
            </li>
            <li v-if="!isLoggedIn">
              <router-link to="/register">Register</router-link>
            </li>
            <li v-if="isLoggedIn">
              <button class="btn darken-4" @click="logout">Logout</button>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/firebase-auth";
export default {
  name: "Navbar",
  data() {
    return {
      isLoggedIn: false,
      currentUser: false
    };
  },
  created() {
    if (firebase.auth().currentUser) {
      this.isLoggedIn = true;
      this.currentUser = firebase.auth().currentUser.email;
    }
  },
  methods: {
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.go({ path: this.$router.path });
        });
    }
  }
};
</script>
<style scoped>
.email {
  padding-right: 10px;
}
</style>
