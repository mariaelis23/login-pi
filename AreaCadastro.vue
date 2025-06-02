<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router'
const router = useRouter()

// Campos do formulário
const nome = ref('');
const telefone = ref('');
const email = ref('');
const senha = ref('');

// Função para tratar o envio do formulário
function enviarFormulario(tipo) {
  if (!nome.value || !telefone.value || !email.value || !senha.value) {
    alert("Preencha todos os campos.");
    return;
  }

  // Cria objeto user e salva no localStorage
  const user = {
    nome: nome.value,
    telefone: telefone.value,
    email: email.value,
    senha: senha.value,
    tipo: tipo
  };

  localStorage.setItem('user', JSON.stringify(user));
  alert('Cadastro realizado com sucesso!');
  router.push('/login');  // Redireciona para login (ajuste se necessário)
}
</script>

<template>
  <div id="div-cadastro">
    <form @submit.prevent="enviarFormulario('cliente')" id="formulario">
      <h1>Faça seu cadastro:</h1>
      <input type="text" id="nome" placeholder="Nome" v-model="nome" required />
      <input type="text" id="telefone" placeholder="Telefone" v-model="telefone" required />
      <input type="email" id="email" placeholder="E-mail" v-model="email" required />
      <input type="password" id="senha" placeholder="Senha" v-model="senha" required />

      <h2>Selecione:</h2>
      <div id="div-enviar">
        <button type="button" @click="enviarFormulario('cliente')" style="width:47%;">Cliente</button>
        <button type="button" @click="enviarFormulario('prestador')" style="width:47%;">Prestador de Serviço</button>
      </div>

      <RouterLink to="/login">Já tenho uma conta</RouterLink>
    </form>
  </div>
</template>
