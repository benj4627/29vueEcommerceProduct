<script setup>
//imports 
import { ref } from 'vue';
import TheHeader from './components/TheHeader.vue';
import ProductDescription from './components/ProductDescription.vue';
import ProductImage from './components/ProductImage.vue';

const cartItems = ref([])

//funktioner
function addToCart(item) {
  //Søger efter en vare i kurven med samme navn som den, der forsøges tilføjet (item.name).
  const existingItem = cartItems.value.find(i => i.name === item.name)
  //Hvis varen allerede findes i kurven, opdateres dens quantity med værdien fra den nye vare.
  if (existingItem) {
    existingItem.quantity = item.quantity
    // Hvis varen ikke findes i kurven, tilføjes den som et nyt element i cartItems.
  } else {
    cartItems.value.push(item)
  }
}

const clearCart = () => {
  cartItems.value = []; 
}

</script>

<template>
  <header>
    <!-- Header modtager kurvens varer som en prop og lytter til clearCart-eventen -->
    <TheHeader :cartItems="cartItems" @clearCart="clearCart"/>
  </header>

  <main class="centerContent">
    <section class="imagesContainer">
      <ProductImage/>
    </section>
    <section class="descriptionContainer">
      <!-- Sender funktionen addToCart som en prop til ProductDescription-komponenten -->
      <ProductDescription :addToCart="addToCart"/>
    </section>
  </main>
</template>

<style scoped>
  main {
    display: flex; 
    justify-content: space-between;
    align-items: flex-start;
    width: 80%;
  }

</style>
