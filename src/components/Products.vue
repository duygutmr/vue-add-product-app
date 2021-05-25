<template>
<div v-if="productList.length > 0">
      <h3 class="text-center">Eklenen Ürünlerin Listesi</h3>
    <hr>
      <div class="row product-container">
    <product v-for="product in productList" :key="product.id">
      <img
        class="card-img-top"
        :src="product.selectedImage"
        :alt="product.title"
      />
      <div class="card-body">
        <h5 class="card-title">{{ product.title }}</h5>
        <small>
          <strong>Adet : {{ product.count }} </strong>
        </small>
        <br />
        <small>
          <strong>Fiyat : {{ product.price }}</strong>
        </small>
        <br />
        <small>
          <strong>Tutar : {{ product.totalPrice }}</strong>
        </small>
      </div>
    </product>
  </div>
</div>

</template>

<script>
import { eventBus } from "../main";
import Product from "./Product";

export default {
  components: {
    Product,
  },
  data() {
    return {
      productList: [],
    };
  },
  created() {
    eventBus.$on("productAdded", (product) => {
      if(this.productList.length < 5) {
        this.productList.push(product);
        eventBus.$emit("progressBarUpdated", this.productList.length)
      } else {
        alert("daha fazla ekleyemezsiniz")
      }
    });
  },
};
</script>

<style>
</style>