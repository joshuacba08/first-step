<script setup>
import { ref } from "vue";

// el ref es un objeto que contiene una propiedad value que es reactiva
// por lo cual me permite interpolarla en el template con los cambios que se hagan
const birthday = ref({
  day: 0,
  month: 0,
  year: 0,
});

const handleInput = (e) => {
  console.log(e.target.value);
  console.log(birthday);
};
</script>

<template>
  <main class="main-container">
    <div class="card">
      <!-- form -->
      <form class="form">
        <div class="form-group">
          <label for="">Day</label>
          <input
            v-on:input="handleInput"
            v-model="birthday.day"
            type="number"
          />
        </div>
        <div class="form-group">
          <label for="">Month</label>
          <input v-model="birthday.month" type="number" />
        </div>
        <div class="form-group">
          <label for="">Year</label>
          <input v-model="birthday.year" type="number" />
        </div>
      </form>

      <div>
        <p>{{ birthday.year }} years</p>
        <p>{{ birthday.month }} months</p>
        <p>{{ birthday.day }} days</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
.main-container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  background-color: var(--white);
  padding: 30px 24px;
  border-radius: 12px 12px 100px 12px;
}

.form {
  display: flex;
  gap: 20px;
}
.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  width: 30%;
}

.form-group label {
  text-transform: uppercase;
}

.form-group input {
  width: 80px;
  height: 54px;
  border-radius: 8px;
  border: 1px solid var(--light-grey);
  text-align: center;
  font-size: 1.5rem;
}
</style>
