<template>
  <div id="dashboard">
    <ul class="collection with-header">
      <li class="collection-header"><h4>Employees</h4></li>
      <li v-for="(employee, i) in employees" :key="i" class="collection-item">
        <div class="chip">{{ employee.dept }}</div>
        {{ employee.employee_id }}: {{ employee.name }}

        <router-link
          class="secondary-content"
          :to="{
            name: 'viewemployee',
            params: { employee_id: employee.employee_id }
          }"
        >
          <i class="fa fa-eye"></i
        ></router-link>
      </li>
    </ul>
    <div class="fixed-action-btn ">
      <router-link
        to="/new"
        class="btn-floating btn-large teal lighten-2 pulse"
      >
        <i class="fa fa-plus"></i>
      </router-link>
    </div>
  </div>
</template>

<script>
import db from "./firebaseinit";

export default {
  name: "Dashboard",
  data() {
    return {
      employees: []
    };
  },
  created() {
    const docRef = db.collection("employees");
    docRef
      .orderBy("dept")
      .get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          const data = {
            id: doc.id,
            employee_id: doc.data().employee_id,
            name: doc.data().name,
            dept: doc.data().dept,
            position: doc.data().position
          };
          this.employees.push(data);
        });
      });
  }
};
</script>
