<template>
    <div>
      <h1>Welcome to the ACB Virtual Office!</h1>
      <p class="center">Please register below:</p>
      <div class="form__container">
        <form @submit.prevent="register">

          <!-- Email Field -->
          <div class="form__group">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              v-model="email"
              placeholder="test@acb.studio"
              aria-required="true"
            />
          </div>
  
          <!-- Password Field -->
          <div class="form__group">
            <label for="password">Password</label>
            <div class="password__wrapper">
              <input
                :type="passwordVisible ? 'text' : 'password'"
                id="password"
                v-model="password"
                @input="validatePassword"
                placeholder="Enter your password"
                aria-required="true"
              />
              <button
                type="button"
                @click="togglePasswordVisibility"
                aria-label="Toggle password visibility"
              >
                {{ passwordVisible ? "Hide Password" : "Show Password" }}
              </button>
            </div>
          </div>
  
          <!-- Password Strength Feedback -->
          <div class="password__conditions">
            <ul class="ul__group">
              <li :class="{ valid: conditions.length }">At least 8 characters</li>
              <li :class="{ valid: conditions.special }">Contains special character</li>
              <li :class="{ valid: conditions.number }">Contains number</li>
              <li :class="{ valid: conditions.uppercase }">Contains uppercase letter</li>
              <li :class="{ valid: conditions.lowercase }">Contains lowercase letter</li>
            </ul>
          </div>
  
          <!-- Terms of Service -->
          <div class="formgroup">
            <input
              type="checkbox"
              id="terms"
              v-model="termsAccepted"
            />
            <label for="terms">Accept Terms of Service</label>
          </div>
  
          <!-- Register Button -->
          <button type="submit" :disabled="!isFormValid" aria-label="Register button">
            Register
          </button>
        </form>
        <p class="center">Made with & &#9829; by Julia Pim Reis</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from "vue";
  
  const email = ref("");
  const password = ref("");
  const passwordVisible = ref(false);
  const termsAccepted = ref(false);
  
  const conditions = ref({
    length: false,
    special: false,
    number: false,
    uppercase: false,
    lowercase: false,
  });
  
  const validatePassword = () => {
    const specialCharRegex = /[!@#$%^&*(),.?":{}|<>]/;
    const numberRegex = /\d/;
    const uppercaseRegex = /[A-Z]/;
    const lowercaseRegex = /[a-z]/;
  
    conditions.value.length = password.value.length >= 8;
    conditions.value.special = specialCharRegex.test(password.value);
    conditions.value.number = numberRegex.test(password.value);
    conditions.value.uppercase = uppercaseRegex.test(password.value);
    conditions.value.lowercase = lowercaseRegex.test(password.value);
  };
  
  const togglePasswordVisibility = () => {
    passwordVisible.value = !passwordVisible.value;
  };
  
  const isFormValid = computed(() => {
    return (
      termsAccepted.value &&
      email.value.includes("@")
    );
  });
  
  const register = () => {
    alert("Form Submitted Successfully!");
  };
  </script>
  
  <style scoped>
  .center {
    text-align: center;
    padding: 0.5rem;
  }

  .ul__group{
    display: flex;
    flex-direction: column;
    align-items: baseline;
  }
  
  .form__container {
    max-width: 400px;
    margin: auto;
    padding: 20px;
  }
  
  label {
    font-weight: bold;
  }
  
  input {
    width: 100%;
    padding: 10px;
  }
  
  .password__wrapper {
    position: relative;
  }
  
  .password__conditions {
    margin-top: 10px;
  }
  
  .password__conditions ul {
    padding: 0;
    margin: 10px 0 0;
    list-style: none;
  }
  
  .password__conditions ul li {
    color: red;
  }
  
  .password__conditions ul li.valid {
    color: green;
    list-style:disc;
  }
  
  button {
    width: 100%;
    padding: 10px;
    background-color: gray;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
  }
  
  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
  </style>
  