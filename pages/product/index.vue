<template>
  <div class="app">
    <main>
      <div>
        <input type="text"> 
      </div>
      <div>
        <ul>
          <li
          v-for="product in products"
          :key="product.id"
          class="item flex"
          @click="moveToDetailPage(product.id)">
            <img class="product-image" :src="product.imageUrl" :alt="product.name" >
            <p>{{ product.name }}</p>
            <span>{{ product.price }}</span>
          </li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    async asyncData(){
      // 순서가 매우 중요한 화면일 경우 해당 이벤트훅을 사용한다.
      // asyncData는 페이지컴포넌트에서만 제공된다.
      const response = await axios.get('http://localhost:3000/products');
      const products = response.data.map( item => {
        return {
          ...item,
          imageUrl: `${item.imageUrl}?random=${Math.random()}`
        }
      });
      return { products }
    },
    // data(){
    //   return {
    //     product: []
    //   }
    // },
    async created(){
    },
    methods: {
      moveToDetailPage(id) {
        this.$router.push(`${this.$route.name}/detail/${id}`)
      }
    }
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}
.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}
.product-image {
  width: 400px;
  height: 250px;
}
.app {
  position: relative;
}
.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}
.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>