<template>
  <div class="w-full max-w-xs ml-[30%] pt-5">
    <form class="bg-blue-400 shadow-md rounded px-8 pt-6 pb-8 mb-4" v-on:submit.prevent="submitForm">
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
          Email
        </label>
        <input v-model="form.email" class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="email" type="email" placeholder="email">
      </div>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="firstname">
          Primer Nombre
        </label>
        <input v-model="form.firstname" class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="firstname" type="text" placeholder="Primer Nombre">
      </div>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="lastname">
          Apellidos
        </label>
        <input v-model="form.lastname" class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="lastname" type="text" placeholder="Apellidos">
      </div>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="dni">
          N° de Cédula
        </label>
        <input v-model="form.cedula" class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="dni" type="number" placeholder="N° de cédula">
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
          Contraseña
        </label>
        <input v-model="form.password1" class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password" type="password" placeholder="******************">
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password2">
          Confirmar Contraseña
        </label>
        <input v-model="form.password2" class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline" id="password2" type="password" placeholder="******************">
      </div>
      <template>
        <div class="bg-red-300 text-white rounded-lg p-6">
          <p v-for="error in errors" v-bind:key="error">{{ error }}</p>
        </div>
      </template>
      <div class="flex items-center justify-between">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full focus:outline-none focus:shadow-outline" type="button">
          Registrar
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import { useToastStore } from '@/stores/toast'
export default {
  setup() {
    const toastStore = useToastStore()
    return {
      toastStore
    }
  },
  data() {
    return {
      form: {
        email: '',
        cedula: '',
        firstname: '',
        lastname: '',
        password1: '',
        password2: ''
      },
      errors: []
    }
  },
  methods: {
    submitForm() {
      this.errors = []

      if (this.form.email === '') {
        this.errors.push('Email no ha sido encontrado')
      }
      if (this.form.cedula === '') {
        this.errors.push('Cédula no ha sido encontrado')
      }
      if (this.form.firstname === '') {
        this.errors.push('Nombre no ha sido encontrado')
      }
      if (this.form.lastname === '') {
        this.errors.push('Apellido no ha sido encontrado')
      }
      if (this.form.password1 === '') {
        this.errors.push('Contraseña inválida')
      }
      if (this.form.password2 === '') {
        this.errors.push('Contraseña inválida')
      }
      if (this.errors.length === 0) {
        axios.post('/api/signup/', this.form)
          .then(response => ({
            if (response.data.message === 'success') {
              this.toastStore.showToast(5000, 'Usuario registrado, por favor, entre!', 'bg-emerald-green')

              this.form.email = ''
              this.form.firstname = ''
              this.form.cedula = ''
              this.form.lastname = ''
              this.form.password1 = ''
              this.form.password2 = ''
            } else {
              this.toastStore.showToast(5000, 'Algo anda mal, pruebe de nuevo.')
            }
          }).catch(error => ({
            console.log('error', error)
          })
      }
    }
  }
}
</script>
