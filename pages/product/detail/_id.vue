<template>
  <div>
    <h1>
        상세페이지
    </h1>
    <div>
      <img :src="product.imageUrl" :alt="product.name">
      <p>{{ product.name }}</p>
      <p>{{ product.price }}</p>
    </div>
  </div>
</template>

<script>
import { fetchProductById } from '~/api';

export default {
    async asyncData({params}) {
      const response = await fetchProductById(params.id);
      const product = response.data;
      return { product }
    },
    created() {

    }
}
</script>

<style>

</style>