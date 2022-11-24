<template>
  <section>
    <div class="container mx-auto">
      <Form @submit="submitForm" :validation-schema="schema" v-slot="{ errors }">
        <label for="nama">Nama</label>
        <Field type="text" name="nama" v-model="form.nama" :validateOnInput="true"></Field>
        <p>{{ errors.nama }}</p>

        <button type="submit">submit</button>
      </Form>
    </div>
  </section>
</template>

<script setup>
import { Form, Field } from 'vee-validate'
import { reactive } from 'vue'
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

</script>