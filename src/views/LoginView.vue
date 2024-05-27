<script setup>
import { ref } from 'vue';
import supabase  from '../supabase';
// connect input's
let email = ref('');
let password = ref('');
let errorMsg = ref('');
let userLogin = ref('')
// Account form create



// Login


async function Login() {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value

  })
  if (error) {
    errorMsg.value = "Usuario o Contraseña Incorrectas!"
  }
  else{
   userLogin = (data)
  }
}

// See current User
async function seeCurrentUser() {
  const localUser = await supabase.auth.getSession();
  console.log(localUser)
}

// Logout
async function logout() {
  const { error } = await supabase.auth.signOut();
  if (error) {
    console.log(error);
  } 
  else{
    console.log("logout")
  }
}


// Get User



</script>

<template>
    <h1>{{userLogin}}</h1>
  <div v-if="errorMsg" id="toast-default" class="flex items-center w-full max-w-xs p-4 text-gray-500 bg-white rounded-lg shadow dark:text-gray-400 dark:bg-gray-800" role="alert">
    <div class="inline-flex items-center justify-center flex-shrink-0 w-8 h-8 text-blue-500 bg-blue-100 rounded-lg dark:bg-blue-800 dark:text-blue-200">
        <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 20">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.147 15.085a7.159 7.159 0 0 1-6.189 3.307A6.713 6.713 0 0 1 3.1 15.444c-2.679-4.513.287-8.737.888-9.548A4.373 4.373 0 0 0 5 1.608c1.287.953 6.445 3.218 5.537 10.5 1.5-1.122 2.706-3.01 2.853-6.14 1.433 1.049 3.993 5.395 1.757 9.117Z"/>
        </svg>
        <span class="sr-only">Fire icon</span>
    </div>
    <div class="ms-3 text-sm font-normal">{{errorMsg}}</div>
    <button type="button" class="ms-auto -mx-1.5 -my-1.5 bg-white text-gray-400 hover:text-gray-900 rounded-lg focus:ring-2 focus:ring-gray-300 p-1.5 hover:bg-gray-100 inline-flex items-center justify-center h-8 w-8 dark:text-gray-500 dark:hover:text-white dark:bg-gray-800 dark:hover:bg-gray-700" data-dismiss-target="#toast-default" aria-label="Close">
        <span class="sr-only">Close</span>
        <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"/>
        </svg>
    </button>
</div>
  
  <div class="w-full max-w-xs ml-[30%] pt-5">
    <form  class="bg-blue-400 shadow-md rounded px-8 pt-6 pb-8 mb-4">
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
         Correo
        </label>
        <input v-model="email"
          class="shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          id="email" type="email" placeholder="Correo">
      </div>
      
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
          Contraseña
        </label>
        <input v-model="password"
          class=" shadow appearance-none border hover:border-blue-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          id="password" type="password" placeholder="******************">

      </div>
      <div class="flex items-center justify-between">
        <button @click="Login"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full focus:outline-none focus:shadow-outline"
          type="button">
          Login
        </button>
        <button @click="logout"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full focus:outline-none focus:shadow-outline"
          type="button">
          logout
        </button>
        <a class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800" href="#">
          Olvido la contraseña?
        </a>
      </div>
    </form>
  </div>

</template>

