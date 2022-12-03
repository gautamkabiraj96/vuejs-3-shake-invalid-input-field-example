<script setup>
import { ref } from 'vue';

const isInputInvalid = ref(false);
const inputPasswordValue = ref('');

const checkInputValidity = () => {
    isInputInvalid.value = inputPasswordValue.value.length < 8

    if(isInputInvalid.value) {
      shakeInputField()
    } else {
      document.querySelector('.input-password').classList.remove('invalid-password')
      alert('Success!')
    }
}

const shakeInputField = () => {
  document.querySelector('.input-password').classList.add('invalid-password')
  setTimeout(() => {
      document.querySelector('.input-password').classList.remove('invalid-password')
  }, 1000)
}
</script>

<template>
<div>
    <h2>
      Enter password
    </h2>
    <input 
      type="password" 
      class="input-password"
      v-model="inputPasswordValue" />
    <p v-if="isInputInvalid">
      Password should be at least 8 characters long!
    </p>
    <div>
      <button @click="checkInputValidity">Submit</button>
    </div>
</div>
</template>

<style scoped>
.input-password {
    font-size: 16px;
    letter-spacing: 3px;
    padding: 4px 6px;
    outline: none;
    border: 1px solid #000;
}

.invalid-password {
  border: 1px solid red;
  animation-name: shake-input;
  animation-iteration-count: infinite;
  animation-duration: 0.2s;
}

@keyframes shake-input {
  0% {
    transform: translateX(-10px)
  }
  25% {
    transform: translateX(0px)
  }
  50% {
    transform: translateX(10px)
  }
  75% {
    transform: translateX(0px)
  }
  100% {
    transform: translateX(-10px)
  }
}
</style>