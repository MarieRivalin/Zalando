<script setup>
import Header from './components/Header-zalando.vue'
import Footer from './components/Footer-test.vue'
import Details from './components/Details-test.vue'

import data from './assets/data.json'

import { reactive, ref } from 'vue'

const productInfos = reactive(data)

const selectedVariant = ref(data.variants[0])
const cart = reactive([])

const changeVariant = (variant) => {
  selectedVariant.value = variant
}

const addToCart = () => {
  cart.push(selectedVariant)
}
</script>

<template>
  <div>
    <Header :cart="cart" />
    <main>
      <div class="container">
        <div>
          <img :src="selectedVariant.image.url" :alt="selectedVariant.image.alt" />
        </div>

        <Details
          @addProductToCart="addToCart"
          @changeSelectedVariant="changeVariant"
          v-bind:productInfos="productInfos"
          v-bind:selectedVariant="selectedVariant"
        />
      </div>
    </main>

    <Footer />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  height: calc(
    100vh - var(--header-top-height) - var(--header-bottom-height) - var(--footer-height)
  );
}
.container > div {
  /*border: 1px solid red;*/
  width: 50%;
}
.container > div:last-child {
  padding: 25px 0 25px 100px;
}
.container > div:first-child {
  padding: 25px;
}
img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
