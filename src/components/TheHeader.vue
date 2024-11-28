<script setup>
import { ref, computed  } from 'vue';

//modtager props fra parent komponent.
const props = defineProps({
  cartItems: {
    type: Array,
    required: true
  }
})

//ref til at styre visning af kurve
let cartToggle = ref(false)

//beregner samlet antal varer i kurven. 
const totalItems = computed(() => {
    //reduce går gennem alle varer i cartItems og lægger værdien af deres quantity sammen for at finde det samlede antal varer i kurven.
    return props.cartItems.reduce((total, item) => total + item.quantity, 0)
})

//funktion til at vise kurven når den trykkes på
function toggleCart() {
  cartToggle.value = !cartToggle.value;
}

//emit til at rydde kurven
const emit = defineEmits(['clearCart'])

//sender funktion til parent component.
function clearAll() {
  emit('clearCart'); 
}


</script>

<template>
    <section class="navContainer centerContent">
        <div class="leftContent">
            <a href="#">
                <img src="../assets/images/logo.svg" alt="Sneakers logo">
            </a>
            <ul>
                <li class="hoverBorderBottom"><a href="#">Collections</a></li>
                <li class="hoverBorderBottom"><a href="#">Men</a></li>
                <li class="hoverBorderBottom"><a href="#">Women</a></li>
                <li class="hoverBorderBottom"><a href="#">About</a></li>
                <li class="hoverBorderBottom"><a href="#">Contact</a></li>
            </ul>
        </div>
        <div class="rightContent">
            <div @click="toggleCart" class="cartIcon">
                <img src="../assets/images/icon-cart.svg" alt="Shopping cart logo">
                <Transition name="fade">
                    <span v-if="totalItems > 0" class="cartItemCount">
                        {{ totalItems }}
                    </span>
                </Transition>
            </div>
            <div class="profilePicContainer">
                <img src="../assets/images/image-avatar.png" alt="profile picture">
            </div>
        </div>

        
    <Transition name="fade">
      <div v-show="cartToggle" class="cartContentContainer">
        <p class="cartTitle">Cart</p>
        <div class="cartContent">
            <ul class="cartUl" v-if="props.cartItems.length > 0">
                <li class="cartItemLi" v-for="item in props.cartItems" :key="item.name">
                    <div class="cartItemDetails">
                        <p class="nameItemCart">{{ item.name }}</p>
                        <div class="cartFlexPrice">
                            <div class="cartProductImg">
                                <img src="../assets/images/image-product-1-thumbnail.jpg" alt="">
                            </div>
                            <p class="itemPriceCart">${{ item.price }} x {{ item.quantity }}</p>
                            <p class="itemPriceXQuantity">${{ item.price * item.quantity }}</p>
                        </div>
                </div>
                <button @click="clearAll" class="removeItemBtn"><img src="../assets/images/icon-delete.svg" alt=""></button>
                </li>
                <button class="checkOutBtn">Checkout</button>
            </ul>
            <p v-else>Your cart is empty.</p>
            </div>
      </div>
    </Transition>

    </section>
</template>

<style scoped>

    .cartItemCount {
        position: absolute;
        top: 20px;
        right: 50px;
        background-color: var(--orange);
        color: white;
        border-radius: 50%;
        padding: .5em 1em;
        font-size: .8rem
    }

    .cartTitle {
        font-weight: bold;
        font-size: 1.5rem;
    }

    .cartProductImg img {
        height: 8vh;
        border-radius: 10px;
    }

    .cartContent {
        padding: 20px;
        width: 22vw;
    }

    .cartUl {
        list-style-type: none;
        padding: 0;
        margin: 0;
        display: flex;
        flex-direction: column; 
        justify-content: center;
    }

    .cartItemLi {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 15px 0;
        border-bottom: 1px solid #ddd;
    }

    .cartItemDetails {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }

    .nameItemCart {
        font-size: 16px;
        font-weight: bold;
        margin-bottom: 5px;
    }

    .cartFlexPrice {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
    }

    .itemPriceCart {
        font-size: 14px;
        color: #888;
    }

    .itemPriceXQuantity {
        font-size: 14px;
        font-weight: bold;
    }

    .removeItemBtn {
        border: none;
        font-size: 20px;
        cursor: pointer;
        transition: .3s ease-in-out
    }

    .removeItemBtn:hover {
        transform: scale(125%);
    }

    .checkOutBtn {
        margin-top: 1rem;
        background-color: var(--orange);
        padding: .6em 3em;
        color: var(--darkGrayBlue);
        border-radius: var(--borderRadius);
        border: 2px solid var(--orange);
        font-weight: bold;
        transition: .3s ease-in-out;
    }

    .checkOutBtn:hover {
        background-color: var(--paleOrange);
        border: 2px solid var(--paleOrange);
        transform: scale(105%);
        cursor: pointer;
    }

    .fade-enter-active,
    .fade-leave-active {
        transition: 0.5s ease-in-out;
    }

    .fade-enter,
    .fade-leave-to {
        opacity: 0;
    }

    .navContainer {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: var(--largeSpacing) 0;
        position: relative;
        margin-bottom: 8rem;
    }

    .cartContentContainer {
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 5px 8px rgba(0, 0, 0, 0.06);
        width: 25vw;
        height: fit-content;
        background-color: var(--lightGrayBlue);
        padding: var(--largeSpacing);
        position: absolute;
        right: 0;
        top: 100px;
        border-radius: var(--borderRadius);
    }

    .cartContent p  {
        text-align: center;
    }

    .leftContent {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 4em;
    }

    .leftContent ul {
        display: flex;
        gap: var(--largeSpacing);
        justify-content: center;
        align-items: center
    }

    .leftContent li {
        transition: .3s ease-in-out;
        list-style-type: none;
    }

    .leftContent a {
        color: var(--grayBlue);
        transition: .3s ease-in-out;
    }

    .leftContent li:hover,  .leftContent img:hover {
        transform: scale(105%);
        color: var(--grayBlue);
    }

    .leftContent a:hover {
        color: var(--darkBlue);
    }

    .hoverBorderBottom {
        display: inline-block;
        position: relative;
        padding: 10px 20px;
        font-size: 16px;
        color: var(--orange);
        text-decoration: none;
        cursor: pointer;
        transition: color 0.3s ease;
    }

    .hoverBorderBottom::after {
        content: "";
        position: absolute;
        bottom: -5px;
        left: 0;
        width: 0;
        height: 2.5px;
        background: var(--orange);
        transition: width 0.3s ease;
    }

    .hoverBorderBottom:hover::after {
        width: 100%;
    }


    .leftContent img {
        transition: .3s ease-in-out
    }

    .rightContent {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: var(--largeSpacing);
    }

    .profilePicContainer img {
        height: 5vh;
        transition: .3s ease-in-out;
        border-radius: 100%;
        padding: 2px;
    }

    .cartIcon img {
        transition: .3s ease-in-out;
    }

    .profilePicContainer img:hover {
        transform: scale(110%);
    }

    .cartIcon img:hover {
        transform: scale(120%);
        cursor: pointer;
       
    }

    .profilePicContainer img:hover {
        background-color: var(--orange);
        
    }
</style>