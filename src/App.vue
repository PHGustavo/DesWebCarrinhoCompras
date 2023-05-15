<script setup>
import { ref } from 'vue'

const listaCompras1 = ref([
  {
    id: 1,
    nome: 'Camiseta',
    preco: 49.9,
    imagem: 'https://m.media-amazon.com/images/I/415M8ksnThL._AC_UL320_.jpg',
    enviar: '',
    quantidade: 0
  },
  {
    id: 2,
    nome: 'Calça',
    preco: 99.9,
    imagem:
      'https://d2yz13iov9gk4s.cloudfront.net/Custom/Content/Products/58/75/58751_calca-jeans-masculina-pr-14797-v22-36016_m1_637739656759275728.png',
    enviar: '',
    quantidade: 0
  },
  {
    id: 3,
    nome: 'Meia',
    preco: 9.9,
    imagem: 'https://m.media-amazon.com/images/I/61lnuqMeziL._AC_UL320_.jpg',
    enviar: '',
    quantidade: 0
  },
  {
    id: 4,
    nome: 'Tênis',
    preco: 199.9,
    imagem:
      'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ-KIXliTPrYK43qyP8QOyY6YgsFB6BqxmbVg&usqp=CAU',
    enviar: '',
    quantidade: 0
  },
  {
    id: 5,
    nome: 'Boné',
    preco: 29.9,
    imagem:
      'https://a-static.mlcdn.com.br/800x560/bone-liso-preto-basico-fitao-unissex-aba-curva-ajuste-metal-scott-co/bonemania/12267076460/35870144ac8cb230f98773363b8068c6.jpg',
    enviar: '',
    quantidade: 0
  },
  {
    id: 6,
    nome: 'Óculos',
    preco: 99.9,
    imagem:
      'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQpvrkZBF-ZHT8extTzT8xlPOEX5LaO5AOjwA&usqp=CAU',
    enviar: '',
    quantidade: 0
  },
  {
    id: 7,
    nome: 'Relógio',
    preco: 299.9,
    imagem: 'https://m.media-amazon.com/images/I/81M8JQjrf1L._AC_SX679_.jpg',
    enviar: '',
    quantidade: 0
  },
  {
    id: 8,
    nome: 'Bermuda',
    preco: 79.9,
    imagem: 'https://m.media-amazon.com/images/I/51G3eAZ045S._AC_UL320_.jpg',
    enviar: '',
    quantidade: 0
  },
  {
    id: 9,
    nome: 'Cueca',
    preco: 19.9,
    imagem:
      'https://global.cdn.magazord.com.br/levok/img/2022/02/produto/1265/2200104-1.png?ims=fit-in/635x865/filters:fill(white)',
    enviar: '',
    quantidade: 0
  },
  {
    id: 10,
    nome: 'Moletom',
    preco: 199.9,
    imagem: 'https://cf.shopee.com.br/file/75f7ded02d4110fb01aea1fcd9abb76e',
    enviar: '',
    quantidade: 0
  }
])

const carrinhos = ref({
  items: [],
  total: 0
})

function incrementar(index) {
  listaCompras1.value[index].quantidade++
}
function decrementar(index) {
  if (listaCompras1.value[index].quantidade > 0) {
    listaCompras1.value[index].quantidade--
  }
}

function adicionar(index) {
  if (listaCompras1.value[index].quantidade > 0) {
    carrinhos.value.items.push({
      ...listaCompras1.value[index],
      preco: listaCompras1.value[index].quantidade * listaCompras1.value[index].preco
    })

    carrinhos.value.total =
      carrinhos.value.total +
      listaCompras1.value[index].preco * listaCompras1.value[index].quantidade
  }
}

const mostrarCarrinho = ref(false)
const mostrarItems = ref(true)
</script>

<template>
  <div>
    <button @click="mostrarCarrinho = !mostrarCarrinho">Carrinho</button>
  </div>
  <div class="box" v-if="mostrarItems = !mostrarCarrinho">
    <div class="item" v-for="(item, index) in listaCompras1" :key="item.id">
      <p>Item: {{ item.nome }}</p>
      <p>Preco: R${{ item.preco.toFixed(2) }}</p>
      <p>quantidade: {{ item.quantidade }}</p>

      <img :src="item.imagem" />

      <div class="botao">
        <button @click="decrementar(index)">-</button>
        <button @click="incrementar(index)">+</button> <br />
        <button @click="adicionar(index)">Adicionar</button>
      </div>
    </div>
  </div>

  <div class="carrinho" v-if="mostrarCarrinho">
    <div class="item" v-for="item in carrinhos.items" :key="item.id">
      <p>Item: {{ item.nome }}</p>
      <p>Preco: {{ item.preco.toFixed(2) }}</p>
      <p>Quantidade: {{ item.quantidade }}</p>
      <img :src="item.imagem" />
    </div>
    <p>Total:{{ carrinhos.total.toFixed(2) }}</p>
  </div>
</template>

<style scoped>
.box {
  border-style: double;
  display: grid;
  grid-template-columns: 400px 400px 400px;
}

.item {
  margin-top: 50px;
  border-style: groove;
  margin-right: 25px;
  margin-left: 25px;
  align-items: center;
  margin-bottom: 50px;
}

p {
  text-align: center;
}

.botao {
  text-align: center;
  border-style: groove;
  margin-left: 75px;
  margin-right: 75px;
}
img {
  border-style: groove;
  width: 100px;
  height: 150px;
  text-align: center;
  margin-left: 120px;
  margin-right: 75px;
}
</style>
