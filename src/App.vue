<!-- tutorial website https://www.taniarascia.com/getting-started-with-vue/#vue-cli -->
<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <!-- @ tells to perform an action when an event occurs -->
    <employee-form @add:employee="addEmployee" />
    <employee-table :employees="employees" @delete:employee="deleteEmployee" />
  </div>
</template>

<script>
import EmployeeTable from "@/components/EmployeeTable.vue";
import EmployeeForm from "@/components/EmployeeForm.vue";

export default {
  name: "app",
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: "Richard Hendricks",
          email: "richard@piedpiper.com",
        },
        {
          id: 2,
          name: "Bertram Gilfoyle",
          email: "gilfoyle@piedpiper.com",
        },
        {
          id: 3,
          name: "Dinesh Chugtai",
          email: "dinesh@piedpiper.com",
        },
      ],
    };
  },
  methods: {
    addEmployee(employee) {
      // gives new employee id based of position in array
      const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };
      // retrieves event from child which is in EmployeeForm in this case
      this.employees = [...this.employees, newEmployee];
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter((employee) => employee.id !== id);
    },
  },
};
</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}

.small-container {
  max-width: 680px;
}
</style>
