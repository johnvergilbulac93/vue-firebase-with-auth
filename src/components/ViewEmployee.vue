<template>
  <div id="view-employee">
    <ul class="collection with-header">
      <li class="collection-header">
        <h4>{{ name }}</h4>
      </li>
      <li class="collection-item">Employee ID#: {{ emp_id }}</li>
      <li class="collection-item">Department: {{ dept }}</li>
      <li class="collection-item">Position: {{ position }}</li>
    </ul>
    <router-link class="btn grey" to="/">back</router-link> &nbsp;
    <button @click="deleteEmployee" class="btn red" to="/">Delete</button>

    <div class="fixed-action-btn ">
      <router-link
        :to="{ name: 'editemployee', params: { employee_id: employee_id } }"
        class="btn-floating btn-large teal lighten-2 pulse"
      >
        <i class="fa fa-pen"></i>
      </router-link>
    </div>
  </div>
</template>

<script>
import db from "./firebaseinit";

export default {
  name: "View-Employee",
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
    deleteEmployee() {
      const docRef = db.collection("employees");
      if (confirm("Are your sure?")) {
        docRef
          .where("employee_id", "==", this.employee_id)
          .get()
          .then(querySnapshot => {
            querySnapshot.forEach(doc => {
              doc.ref.delete();
              this.$router.push("/");
            });
          });
      }
    }
  },
  created() {
    //     console.log(this.employee_id);
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
