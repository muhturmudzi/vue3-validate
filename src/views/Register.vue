<template>
  <section>
    <div class="container mx-auto">
      <Form @submit="submitForm" :validation-schema="schema" v-slot="{ errors }">
        <label for="nama">Nama</label>
        <Field type="text" name="nama" v-model="form.nama" :validateOnInput="true"></Field>
        <p>{{ errors.nama }}</p>

        <button type="submit">submit</button>
      </Form>

      <p v-if="counting" id="timer">00:30</p>
      <a v-else href="javascript:void(0)" @click="resendOtp">Resend Otp</a>
    </div>
  </section>
</template>

<script setup>
import { Form, Field } from 'vee-validate'
import { reactive, ref } from 'vue'
import * as yup from 'yup'

const form = reactive({
  nama: '',
  email: '',
  password: ''
})

const schema = yup.object().shape({
  nama: yup.string().required()
})

const submitForm = () => {
  console.log('form submitted')
}

const interval = ref(null)
const counting = ref(null)

const startTimer = (duration) => {
  counting.value = true
  let timer = duration
  let minutes
  let seconds

  interval.value = setInterval(() => {
    minutes = parseInt(timer / 60, 10)
    seconds = parseInt(timer % 60, 10)

    minutes = minutes < 10 ? "0" + minutes : minutes
    seconds = seconds < 10 ? "0" + seconds : seconds

    let display = document.querySelector('#timer')
    console.log(display, 'display')

    if (!display) {
      counting.value = false
      clearInterval(interval.value)
      return
    }
    
    display.textContent = `${minutes}:${seconds}`

    if (--timer < 0 || !display) {
      display.textContent = ''
      counting.value = false
      clearInterval(interval.value)
    }
  }, 1000)
}

startTimer(30)

const resendOtp = () => {
  console.log('hallo')
}
</script>