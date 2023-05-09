<script setup>
import { ref } from 'vue';

  const novoItem = ref({
    nome: '',
    preco: 0,
    id: 0,
  })

  const carrinho = ref([])
  const produtos = [
    {
        id: 1,
        nome: 'Camiseta',
        preco: 49.90
    },
    {
        id: 2,
        nome: 'Calça',
        preco: 99.90
    },
    {
        id: 3,
        nome: 'Meia',
        preco: 9.90
    },
    {
        id: 4,
        nome: 'Sapato',
        preco: 199.90
    },
    {
        id: 5,
        nome: 'Boné',
        preco: 29.90
    },
    {
        id: 6,
        nome: 'Óculos',
        preco: 99.90
    },
    {
        id: 7,
        nome: 'Relógio',
        preco: 299.90
    },
    {
        id: 8,
        nome: 'Bermuda',
        preco: 79.90
    },
    {
        id: 9,
        nome: 'Cueca',
        preco: 19.90
    },
    {
        id: 10,
        nome: 'Meia',
        preco: 9.90
    }
]
  
  function adicionar(index) {
    novoItem.value.nome = produtos[index].nome
    novoItem.value.id = produtos[index].id
    novoItem.value.preco = produtos[index].id
    carrinho.value.push(novoItem.value)
  }

  function remover(index) {
    carrinho.value.splice(index, 1)
  }


</script>

<template>



 <ul>
    <li v-for="(item, index) in produtos">{{ item }} <button @click="adicionar(index)">adicionar</button></li>
  </ul>

  <div class="carrinho">
    <ul>
    <li v-for="(item, index) in carrinho">{{ JSON.stringify(item) }} <button @click="remover(index)">Remover</button></li>
  </ul>
  </div>

</template>

<style scoped>

</style>
