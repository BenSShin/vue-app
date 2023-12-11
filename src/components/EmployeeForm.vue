<template>
  <div id="employee-form">
    <!-- @submit is same as v-on:submit or onsubmit -->
    <form @submit.prevent="handleSubmit">
      <label>Employee name</label>
      <!-- v-model is built in Vue and updates an input value with an onchange event -->
      <!-- ref targets a specific element in this case the first element -->
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="employee.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      />
      <label>Employee Email</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        v-model="employee.email"
        @focus="clearStatus"
      />
      <!-- v-if is a contintional in Vue and v-else0if and v-else work the same as in js -->
      <p v-if="error && submitting" class="error-message">❗Please fill out all required fields</p>
      <p v-if="success" class="success-message">✅ Employee successfully added</p>
      <button>Add Employee</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  methods: {
    handleSubmit() {
      console.log("testing handleSubmit");
      // $emit broadacasts a name of an event and data to its parent component
      // this.error and if statements are validations for the inputs
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:employee", this.employee);
      // this will now focus on the first field in the form
      this.$refs.first.focus();
      this.employee = {
        name: "",
        email: "",
      };
      this.error = false;
      this.success = true;
      this.submitting = false;
    },

    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  // computed functions are automaticaly compute when something changes
  computed: {
    invalidName() {
      return this.employee.name === "";
    },

    invalidEmail() {
      return this.employee.email === "";
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}

[class*="-message"] {
  font-weight: 500;
}

.error-message {
  color: #d33c40;
}

.success-message {
  color: #32a95d;
}
</style>
