<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

import { onMounted, ref } from "@vue/runtime-core";
const multiStepForm = ref(null);

onMounted(() => {
  const formSteps = [...multiStepForm.value.querySelectorAll("[data-step]")];
  let currentStep = formSteps.findIndex((step) => {
    return step.classList.contains("active");
  });

  if (currentStep < 0) {
    currentStep = 0;
    showCurrentStep();
  }

  multiStepForm.value.addEventListener("click", (e) => {
    let incrementor;
    if (e.target.matches("[data-next]")) {
      incrementor = 1;
    } else if (e.target.matches("[data-previous]")) {
      incrementor = -1;
    }

    if (incrementor == null) {
      return;
    }
    const inputs = [...formSteps[currentStep].querySelectorAll("input")];
    const allValid = inputs.every((input) => {
      return input.reportValidity();
    });
    if (allValid) {
      currentStep += incrementor
      showCurrentStep();
    }
  });

  function showCurrentStep() {
    formSteps.forEach((step, index) => {
      step.classList.toggle("active", index === currentStep);
    });
  }
});

const submit = (event) => {
  const { email, password } = Object.fromEntries(new FormData(event.target))
  console.log(email, password);
  const form = Object.fromEntries(new FormData(event.target))
  console.log(form);
}
</script>

<template>
  <form data-multi-step ref="multiStepForm" class="multi-step-form" @submit.prevent="submit">
    <div data-step class="card">
      <h3 class="step-title">This is step 1</h3>
      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" name="email" id="email" />
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" name="password" id="password" minlength="6" />
      </div>
      <button data-next class="btn-secondary flex ml-auto" type="button">Next</button>
    </div>
    <div data-step class="card">
      <h3 class="step-title">This is step 2</h3>
      <div class="form-group">
        <label for="address">Address</label>
        <input type="text" name="address" id="address" />
      </div>
      <div class="form-group">
        <label for="city">City</label>
        <input type="text" name="city" id="city" />
      </div>
      <div class="form-group">
        <label for="zipcode">Zip Code</label>
        <input type="text" name="zipcode" id="zipcode" />
      </div>
      <button data-previous class="btn-secondary" type="button">Previous</button>
      <button data-next class="btn-secondary float-right" type="button">Next</button>
    </div>
    <div data-step class="card">
      <h3 class="step-title">This is step 3</h3>
      <div class="form-group">
        <label for="firstName">First Name</label>
        <input type="text" name="firstName" id="firstName" />
      </div>
      <div class="form-group">
        <label for="lastName">Last Name</label>
        <input type="text" name="lastName" id="lastName" />
      </div>
      <button data-previous class="btn-secondary" type="button">Previous</button>
      <button class="btn-primary float-right" type="submit">Submit</button>
    </div>
  </form>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 3rem;
}
</style>
