<script setup>
import { ref } from 'vue';
import supabase  from '../supabase';
// connect input's
let email = ref('');
let password = ref('');

// Account form create

async function createUser () {
   const { data, error } = await supabase.auth.signUp({
    email: email.value,
    password: password.value
   })
   if ( error ) {
    console.log(error)
   }
   else {
    console.log(data)
   }
}
</script>

<template>
  <div class="w-full max-w-xs ml-[30%] pt-5">
    <form class="bg-blue-400 shadow-md rounded px-8 pt-6 pb-8 mb-4">

      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="correo">
          Correo
        </label>
        <input v-model="email"
          class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="correo" type="email" placeholder="Correo">
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
          Contraseña
        </label>
        <input v-model="password"
          class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          id="password" type="password" placeholder="******************">

      </div>
      <div class="flex items-center justify-between">
        <button @click="createUser"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full focus:outline-none focus:shadow-outline"
          type="button">
          Registrar
        </button>
        <a class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800" href="#">
          Olvido la contraseña?
        </a>
      </div>
    </form>
  </div>

</template>


