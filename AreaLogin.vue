<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router'
const router = useRouter()

const email = ref('');
const senha = ref('');

function enviarFormulario() {
  const user = JSON.parse(localStorage.getItem('user'));

  if (user && user.email === email.value && user.senha === senha.value) {
    localStorage.setItem('loggedInUser', JSON.stringify(user));
    alert('Login bem-sucedido!');
    router.push('/home');  // Ajuste para a rota da página inicial
  } else {
    alert('E-mail ou senha incorretos!');
  }
}
</script>

<template>
  <div id="div-cadastro">
    <form @submit.prevent="enviarFormulario" id="formulario">
      <h1>Insira seu login:</h1>
      <input type="email" id="email" placeholder="E-mail" v-model="email" required />
      <input type="password" id="senha" placeholder="Senha" v-model="senha" required />
      <div id="div-enviar">
        <button type="button" @click="enviarFormulario" style="width:100%;">Login</button>
      </div>
      <RouterLink to="/cadastro">Ainda não possuo uma conta</RouterLink>
    </form>
  </div>
</template>
