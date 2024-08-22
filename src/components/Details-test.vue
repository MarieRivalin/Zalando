<script setup>
const props = defineProps({
  productInfos: {
    type: Object,
    required: true
  },
  selectedVariant: {
    type: Object,
    required: true
  }
})

const isVariantSoldOut = (sizes) => {
  for (const key in sizes) {
    if (sizes[key] > 0) return false
  }
  return true
}
console.log(props)

const emit = defineEmits(['changeSelectedVariant', 'addProductToCart'])

const handleEmitNewVariant = (variant) => {
  const isSoldOut = isVariantSoldOut(variant.sizes)
  if (!isSoldOut) {
    emit('changeSelectedVariant', variant)
  }
}

const handleSelectSize = (size, quantity) => {
  const newObj = { ...props.selectedVariant }

  if (quantity > 0) {
    newObj.selectedSize = size

    emit('changeSelectedVariant', newObj)
  }
}

const handleAddToCart = () => {
  if (!props.selectedVariant.selectedSize) {
    alert('Veuillez sélectionner une taille')
  } else {
    emit('addProductToCart')
  }
}
</script>

<template>
  <div>
    <div>
      <h2>{{ productInfos.brand }}</h2>
      <h1>{{ productInfos.name }}</h1>
      <p>{{ productInfos.price }} € <span>TVA incluse</span></p>
    </div>
    <div class="rate">
      <font-awesome-icon :icon="['fas', 'star']" />
      <font-awesome-icon :icon="['fas', 'star']" />
      <font-awesome-icon :icon="['fas', 'star']" />
      <font-awesome-icon :icon="['fas', 'star']" />
      <font-awesome-icon :icon="['fas', 'star-half-alt']" />
      <span>{{ productInfos.rate }}</span>
    </div>

    <p>
      Couleur : <span class="selectedColor">{{ selectedVariant.color }}</span>
    </p>
    <div class="img-bloc">
      <img
        v-for="variant in productInfos.variants"
        :key="variant.id"
        :src="variant.image.url"
        :alt="variant.image.alt"
        :class="{
          selectedImg: variant.id === selectedVariant.id,
          outOfStock: isVariantSoldOut(variant.sizes)
        }"
        @click="handleEmitNewVariant(variant)"
      />
    </div>
    <p class="advise">
      Nous vous recommandons de choisir une taille au-dessus de celle habituelle.
    </p>

    <div class="sizes-bloc">
      <p
        v-for="(quantity, size) in selectedVariant.sizes"
        :key="size"
        :class="{
          outOfStock: quantity === 0,
          selectedSize: size === selectedVariant.selectedSize
        }"
        @click="handleSelectSize(size, quantity)"
      >
        {{ size }}
      </p>
    </div>

    <div class="cart-bloc">
      <button @click="handleAddToCart">Ajouter au panier</button>
      <div><font-awesome-icon :icon="['far', 'heart']" /></div>
    </div>
  </div>
</template>

<style scoped>
h1 + p {
  font-size: 22px;
  margin-bottom: 25px;
}
h1 + p span {
  color: var(--dark-grey);
  font-size: 14px;
  font-weight: lighter;
}

/* -- Rate Bloc -- */
.rate {
  margin-bottom: 40px;
}
.rate svg {
  margin-right: 3px;
}
.selectedColor {
  font-weight: bold;
}

/* -- Images Bloc -- */
.img-bloc {
  margin: 10px 0;
  display: flex;
  gap: 10px;
}

img {
  width: 60px;
  height: 70px;
  object-fit: cover;
}
.selectedImg {
  border: 2px solid black;
}
/* -- Advice -- */
.advise {
  background-color: var(--light-grey);
  padding: 20px;
  font-size: 14px;
  font-weight: lighter;
  margin-bottom: 10px;
  line-height: 20px;
}

/* -- sizes bloc  -- */

.sizes-bloc {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}
.sizes-bloc p {
  border: 1px solid black;
  height: 40px;
  width: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 2px;
  cursor: pointer;
}
.outOfStock {
  opacity: 0.3;
}

.sizes-bloc .selectedSize {
  border-width: 2px;
}
/* -- Cart bloc-- */
.cart-bloc {
  display: flex;
  gap: 10px;
}
.cart-bloc button {
  font-family: inherit;
  font-size: inherit;
  font-weight: bold;
  background-color: var(--main-black);
  color: white;
  flex: 1;
  cursor: pointer;
  border: none;
}
.cart-bloc button:hover {
  opacity: 0.7;
}
.cart-bloc div {
  width: 50px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 2px solid var(--main-black);
  color: var(--main-black);
}
.cart-bloc div:hover {
  border-width: 3px;
}
.cart-bloc svg {
  width: 25px;
  height: 25px;
  cursor: pointer;
}
</style>
