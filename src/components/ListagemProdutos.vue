<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useScreen } from '@/composables/screen';
const produtos = ref([]);

onMounted(async () => {
  const response = await axios.get('https://fakestoreapi.com/products');
  produtos.value = response.data;
});

const formatPrice = (price) => `R$ ${price.toFixed(2).replace('.', ',')}`;

const { browserWidth, deviceWidth, isMobile } = useScreen();

</script>

<template>
  <div>
    <h1>
      Produtos - {{ browserWidth }} - {{ deviceWidth }} - {{ isMobile }}
    </h1>
    <div class="container">
      <div class="card" v-for="produto in produtos" :key="produto.id">
        <h1 class="card--title" :class="isMobile ? 'card-mobile' : ''">{{ produto.title }}</h1>
        <div class="card-content">
          <img class="card--avatar" :src="produto.image" :alt="produto.title" width="100" />
          <div class="container-button">
            <p>{{ formatPrice(produto.price) }}</p>
            <button class="btn">Adicionar ao Carrinho</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.card {
  width: 300px;
  margin: 10px;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

.card--title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
}

.card-content {
  display: flex;
  flex-direction: column;
  align-items: center; 
}

.card--avatar {
  width: 100%;
  border-radius: 8px;
  margin-bottom: 10px;
}

.container-button {
  width: 100%;
  text-align: center;
}

.btn {
  width: 100%;
  padding: 8px;
  border: none;
  border-radius: 8px;
  margin-top: 15px;
  outline: none;
  text-transform: uppercase;
  font-weight: 800;
  letter-spacing: 3px;
  color: #fdfdfd;
  background: #0d740d;
  box-shadow: 0px 10px 40px -12px #16b123;
}
</style>