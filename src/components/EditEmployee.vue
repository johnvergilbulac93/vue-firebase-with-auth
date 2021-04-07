<template>
  <div id="Edit-employee">
    <h3>Edit Employee</h3>
    <div class="row">
      <form @submit.prevent="updateEmployee" class="col s12">
        <div class="row">
          <div class="input-field col s12">
            <input type="text" v-model="emp_id" required disabled />
            <label for="emp_id" class="active">Employee ID#</label>
          </div>
          <div class="input-field col s12">
            <input type="text" v-model="name" required />
            <label for="name" class="active">Name</label>
          </div>
          <div class="input-field col s12">
            <input type="text" v-model="dept" required class="" />
            <label for="dept" class="active">Department</label>
          </div>
          <div class="input-field col s12">
            <input type="text" v-model="position" required />
            <label for="position" class="active">Position</label>
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
  name: "Edit-Employee",
  props: ["employee_id"],
  data() {
    return {
      emp_id: null,
      name: null,
      dept: null,
      position: null
    };
  },
  methods: {
    updateEmployee() {
      const docRef = db.collection("employees");
      docRef
        .where("employee_id", "==", this.employee_id)
        .get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            doc.ref
              .update({
                employee_id: this.emp_id,
                name: this.name,
                dept: this.dept,
                position: this.position
              })
              .then(() => {
                this.$router.push({
                  name: "viewemployee",
                  params: { employee_id: this.emp_id }
                });
              });
          });
        });
    }
  },
  created() {
    const docRef = db.collection("employees");
    docRef
      .where("employee_id", "==", this.employee_id)
      .get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          (this.emp_id = doc.data().employee_id),
            (this.name = doc.data().name),
            (this.dept = doc.data().dept),
            (this.position = doc.data().position);
        });
      });
  }
};
</script>
