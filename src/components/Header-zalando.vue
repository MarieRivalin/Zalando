<script setup>
const props = defineProps({
  cart: {
    type: Array,
    required: true
  }
})
console.log(props)
</script>

<template>
  <Header>
    <div class="header-top">
      <div class="container">
        <p>Essayez d'abord, <span>payez après</span></p>
        <p>LIVRAISON & RETOUR <span>GRATUITS*</span></p>
        <p>Retour et <span>remboursement</span></p>
      </div>
    </div>
    <div class="header-bottom">
      <div class="container">
        <nav>
          <a href="#">Femme</a>
          <a href="#">Homme</a>
          <a href="#">Enfant</a>
        </nav>

        <img src="../assets/img/free-zalando-logo-icon-download.png" alt="logo zalando" />

        <nav>
          <font-awesome-icon :icon="['far', 'user']" />
          <font-awesome-icon :icon="['far', 'heart']" />
          <font-awesome-icon :icon="['fas', 'shopping-bag']" />
          <p class="numOfProduct" v-if="cart.length > 0">{{ cart.length }}</p>
        </nav>
      </div>
    </div>
  </Header>
</template>

<style scoped>
/* Header TOP ------ */
.header-top {
  background-color: var(--light-grey);
}

.header-top .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: var(--header-top-height);
  color: var(--dark-grey);
  font-size: 12px;
}
span {
  color: var(--main-orange);
}

/* Header Bottom ------ */
.header-bottom {
  border-bottom: 1px solid var(--light-grey);
}

.header-bottom .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: var(--header-bottom-height);
}
a {
  color: inherit;
  font-weight: bold;
  padding: 10px 15px;
}
a:first-child {
  background-color: var(--main-black);
  color: white;
}

nav {
  display: flex;
  gap: 10px;
  flex: 1;
}
img {
  width: 155px;
  height: 155px;
}
nav:last-of-type {
  justify-content: flex-end;
  position: relative;
}
svg {
  color: var(--main-black);
  padding: 10px;
  border: 2px solid white;
  cursor: pointer;
}
svg:hover {
  border-color: var(--main-black);
}
.numOfProduct {
  position: absolute;
  top: -2px;
  right: -2px;
  background-color: var(--main-orange);
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 14px;
}
</style>
