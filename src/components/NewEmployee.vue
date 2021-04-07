<template>
  <div id="new-employee">
    <h3>New Employee</h3>
    <div class="row">
      <form @submit.prevent="submitEmployee" class="col s12">
        <div class="row">
          <div class="input-field col s12">
            <input type="text" v-model="emp_id" required />
            <label for="emp_id">Employee ID#</label>
          </div>
          <div class="input-field col s12">
            <input type="text" v-model="name" required />
            <label for="emp_id">Name</label>
          </div>
          <div class="input-field col s12">
            <input type="text" v-model="dept" required class="" />
            <label for="emp_id">Department</label>
          </div>
          <div class="input-field col s12">
            <input type="text" v-model="position" required />
            <label for="emp_id">Position</label>
          </div>
          <button type="submit" class="btn">Submit</button> &nbsp;
          <router-link class="btn red" to="/">Cancel</router-link>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import db from "./firebaseinit";

export default {
  name: "New-Employee",
  data() {
    return {
      emp_id: null,
      name: null,
      dept: null,
      position: null
    };
  },
  methods: {
    submitEmployee() {
      const docRef = db.collection("employees");
      docRef
        .add({
          employee_id: this.emp_id,
          name: this.name,
          dept: this.dept,
          position: this.position
        })
        .then(() => {
          this.$router.push("/");
        })
        .catch(error => console.log(error));
    }
  }
};
</script>
