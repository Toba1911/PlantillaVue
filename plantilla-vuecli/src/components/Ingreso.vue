<template>
  <div class="container mt-5">
    <h2>Formulario de Registro</h2>
    <form @submit.prevent="submitForm" class="mb-5">
      <div class="mb-3">
        <label for="name" class="form-label">Nombre</label>
        <input
          type="text"
          class="form-control"
          id="name"
          v-model="name"
          @input="validateName"
        />
        <div v-if="nameError" class="text-danger">{{ nameError }}</div>
      </div>
      <div class="mb-3">
        <label for="age" class="form-label">Edad</label>
        <input
          type="number"
          class="form-control"
          id="age"
          v-model="age"
          @input="validateAge"
        />
        <div v-if="ageError" class="text-danger">{{ ageError }}</div>
      </div>
      <div class="mb-3">
        <label for="email" class="form-label">Email</label>
        <input
          type="email"
          class="form-control"
          id="email"
          v-model="email"
          @input="validateEmail"
        />
        <div v-if="emailError" class="text-danger">{{ emailError }}</div>
      </div>
      <button type="submit" class="btn btn-primary">Enviar</button>
    </form>

    <table class="table table-bordered" v-if="submittedData.length">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(data, index) in submittedData" :key="index">
          <td>{{ data.name }}</td>
          <td>{{ data.age }}</td>
          <td>{{ data.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      age: '',
      email: '',
      nameError: '',
      ageError: '',
      emailError: '',
      submittedData: []
    };
  },
  methods: {
    validateName() {
      if (!this.name) {
        this.nameError = 'El nombre es requerido.';
      } else if (this.name.length < 5 || this.name.length > 15) {
        this.nameError = 'El nombre debe tener entre 5 y 15 caracteres.';
      } else {
        this.nameError = '';
      }
    },
    validateAge() {
      const age = Number(this.age);
      if (!this.age) {
        this.ageError = 'La edad es requerida.';
      } else if (age < 18 || age > 120) {
        this.ageError = 'La edad debe estar entre 18 y 120 años.';
      } else {
        this.ageError = '';
      }
    },
    validateEmail() {
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!this.email) {
        this.emailError = 'El email es requerido.';
      } else if (!emailPattern.test(this.email)) {
        this.emailError = 'El email no es válido.';
      } else {
        this.emailError = '';
      }
    },
    submitForm() {
      this.validateName();
      this.validateAge();
      this.validateEmail();
      
      if (!this.nameError && !this.ageError && !this.emailError) {
        this.submittedData.push({
          name: this.name,
          age: this.age,
          email: this.email
        });
        this.name = '';
        this.age = '';
        this.email = '';
      }
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
}
</style>
