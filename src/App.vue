<script setup>
import { reactive, ref } from "vue";

const birthday = {
  day: null,
  month: null,
  year: null,
};

const birthdayResult = reactive({
  years: "--",
  months: "--",
  days: "--",
});

const birthdayErrors = reactive({
  day: {
    error: false,
    message: "",
  },
  month: {
    error: false,
    message: "",
  },
  year: {
    error: false,
    message: "",
  },
});

const handleClick = () => {
  console.log(birthday);
  console.log(birthdayErrors);

  // validaciones para DD
  if (birthday.day > 31 || birthday.day < 1 || birthday.day === null) {
    birthdayErrors.day.error = true;
    birthdayErrors.day.message = !birthday.day
      ? "This field is required"
      : "Must be a valid day";
  } else {
    birthdayErrors.day.error = false;
    birthdayErrors.day.message = "";
  }

  // validaciones para MM
  if (birthday.month === null || birthday.month < 1 || birthday.month > 12) {
    birthdayErrors.month.error = true;
    birthdayErrors.month.message = !birthday.month
      ? "This field is required"
      : "Must be a valid month";
  } else {
    birthdayErrors.month.error = false;
    birthdayErrors.month.message = "";
  }

  // validaciones para YYYY
  const currentYear = new Date().getFullYear(); // 2023
  if (
    birthday.year === null ||
    birthday.year < 0 ||
    birthday.year > currentYear
  ) {
    birthdayErrors.year.error = true;
    birthdayErrors.year.message =
      birthday.year === null
        ? "This field is required"
        : "Must be a valid year";
  } else {
    birthdayErrors.year.error = false;
    birthdayErrors.year.message = "";
  }


  if(!birthdayErrors.day.error && !birthdayErrors.month.error && !birthdayErrors.year.error) {
  
    const currentDate = new Date();
    const parcialDate = new Date(`${birthday.year}-${birthday.month}-${birthday.day} GMT-03:00`);
    const dateDiff = new Date(currentDate.getTime() - parcialDate.getTime());
    birthdayResult.years = dateDiff.getFullYear() - 1970;
    birthdayResult.months = dateDiff.getMonth();
    birthdayResult.days = dateDiff.getDate() - 1;

  }
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
            v-bind:class="birthdayErrors.day.error ? 'input-error' : ''"
            type="number"
            placeholder="DD"
            v-model="birthday.day"
          />
          <span>{{ birthdayErrors.day.message }}</span>
        </div>
        <div class="form-group">
          <label for="">Month</label>
          <input
            v-bind:class="birthdayErrors.month.error ? 'input-error' : ''"
            type="number"
            placeholder="MM"
            v-model="birthday.month"
          />
          <span>{{ birthdayErrors.month.message }}</span>
        </div>
        <div class="form-group">
          <label for="">Year</label>
          <input
            v-bind:class="birthdayErrors.year.error ? 'input-error' : ''"
            type="number"
            placeholder="YYYY"
            v-model="birthday.year"
          />
          <span>{{ birthdayErrors.year.message }}</span>
        </div>
      </form>

      <div class="divisor-container">
        <hr class="divisor" />
        <button v-on:click="handleClick" class="divisor__button">
          <img src="./assets/images/icon-arrow.svg" />
        </button>
      </div>

      <div class="result-container">
        <p class="result-container__item">
          <span>
            {{ birthdayResult.years }}
          </span>
          years
        </p>
        <p class="result-container__item">
          <span>
            {{ birthdayResult.months }}
          </span>
          months
        </p>
        <p class="result-container__item">
          <span>
            {{ birthdayResult.days }}
          </span>
          days
        </p>
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
  width: 100px;
  height: 54px;
  border-radius: 8px;
  border: 1px solid var(--light-grey);
  text-align: center;
  font-size: 1.5rem;
  font-weight: bold;
}

.form-group span {
  color: var(--light-red);
  font-size: 0.6rem;
  font-style: italic;
}

.divisor-container {
  position: relative;
}
.divisor {
  border: 1px solid var(--light-grey);
  margin: 40px 0;
}
.divisor__button {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  width: 60px;
  height: 60px;
  background-color: var(--purple);
  border-radius: 50%;
  top: -30px;
  right: 0;
}

.divisor__button img {
  width: 36px;
}

.input-error {
  border: 1px solid var(--light-red) !important;
}

.result-container {
}

.result-container__item {
  font-size: 3rem;
  font-weight: 800;
  color: var(--dark-grey);
  font-style: italic;
  line-height: 3.4rem;
}

.result-container__item span {
  color: var(--purple);
}
</style>
