<script setup>
import { ref } from 'vue';
  
  const produtos = ref([
    {
        id: 1,
        nome: 'Camiseta',
        preco: 49.90,
        quantidade: 1
    },
    {
        id: 2,
        nome: 'Calça',
        preco: 99.90,
        quantidade: 1
    },
    {
        id: 3,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 1
    },
    {
        id: 4,
        nome: 'Sapato',
        preco: 199.90, 
        quantidade: 1
    },
    {
        id: 5,
        nome: 'Boné',
        preco: 29.90,
        quantidade: 1
    },
    {
        id: 6,
        nome: 'Óculos',
        preco: 99.90,
        quantidade: 1
    },
    {
        id: 7,
        nome: 'Relógio',
        preco: 299.90,
        quantidade: 1
    },
    {
        id: 8,
        nome: 'Bermuda',
        preco: 79.90,
        quantidade: 1
    },
    {
        id: 9,
        nome: 'Cueca',
        preco: 19.90,
        quantidade: 1
    }
])
  
  let enviar = ref(false)
  let carrinho = ref([])

function addCarrinho(item) {
  const index = carrinho.value.findIndex(x => x.codigo === item.id)
  if (index > -1) {
    alert('item já está no carrinho')
  }
  else {
    carrinho.value.push({
      codigo: item.id,
      nome: item.nome,
      preco: item.preco,
      quantidade: item.quantidade,
      valortotal: item.preco * item.quantidade
    })
    calculacarrinho()
  }

}

let valorcarrinho = ref(0)
function calculacarrinho() {
  valorcarrinho.value = 0
  for (let index = 0; index < carrinho.value.length; index++) {
    valorcarrinho.value = valorcarrinho.value + carrinho.value[index].valortotal
  }
}

function adicionarQuantidade(index) {
  produtos.value[index].quantidade++
}

function removerQuant(index) {
  if (produtos.value[index].quantidade > 1) { produtos.value[index].quantidade-- }
}

function limpacarrinho() {
  carrinho.value = []
  valorcarrinho.value = 0
}
function remover(index) {
  carrinho.value.splice(index, 1)
  calculacarrinho()
}
function vercarrinho() {
  if(carrinho.value < [0]){
    alert('carrinho vazio')
  }
  else{
    enviar.value = !enviar.value
  }
}

const avf = (value) => "R$ " + value.toFixed(2).replace('.', ',')

</script>

<template>
  <div class="itens">
    <h1>Xingiling shops</h1>
    <ul>
      <li v-for="(item, index) in produtos" :key="index">
        <p>Item: {{ item.nome }}</p>
        <p>Valor: {{ avf(item.preco) }}</p>
        <p>Quantidade: {{ item.quantidade }}</p>
        <p><button class="btn btn-primary btn-sm " @click="addCarrinho(item)">adicionar ao carrinho</button>
          <button class="btn btn-primary btn-sm" @click="adicionarQuantidade(item.id - 1)">+</button>
          <button class="btn btn-primary btn-sm" @click="removerQuant(index)">-</button>
        </p>
      </li>
    </ul>
    <button class="btn btn-primary" @click="vercarrinho()">Ver carrinho</button>
  </div>
  <div v-if="enviar" class="carrinho">
    <ul>
      <li v-for="(item, index) in carrinho" :key="index">
        <p>Produto: {{ item.nome }}</p>
        <p>Preço:{{ avf(item.preco) }}</p>
        <p>Quantidade: {{ item.quantidade }}</p>
        <p>valor total {{ avf(item.valortotal) }}</p>
        <button class="btn btn-primary btn-sm" @click="remover(index)">remover</button>
      </li>
    </ul>
    <p>Valor total: {{ avf(valorcarrinho) }}</p>
    <button class="btn btn-primary btn-sm" @click="limpacarrinho()">Limpar carrinho</button> 
    <button class="btn btn-primary btn-sm" @click="enviar = !enviar">Fechar carrinho</button>
  </div>


 

</template>

<style scoped>
ul {
  width: 700px;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-content: center;
  justify-content: space-around;
}

button {
  margin: 3px;
  box-shadow:  -1px 1px 5px rgba(0, 0, 0, 0.733);
  background-color: rgb(189, 189, 189);
  border: 2px rgb(255, 255, 255);
}



</style>
