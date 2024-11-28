<script setup>
import { ref } from 'vue';

const num = ref(1);

//Definerer props, der modtages fra parent komponent
const props = defineProps({
    addToCart: Function
})

//Funktion til at håndtere ændringer i inputværdi fra Element+
const handleChange = (value) => {
    console.log(value);
};


//Funktion til at tilføje en vare til kurven
const addToCart = () => {
    //Kalder addToCart-funktionen, som er modtaget via props, med varedata
    props.addToCart({
        name: 'Fall Limited Edition Sneakers',
        price: 125,
        quantity: num.value
    })
}

</script>

<template>
<section class="descriptionContainer">
    <article>
        <h2 class="brand">SNEAKER COMPANY</h2>
        <h3 class="title">Fall Limited Edition Sneakers</h3>
        <p class="textDescrip"> These low-profile sneakers are your perfect casual wear companion. Featuring a 
        durable rubber outer sole, they’ll withstand everything the weather can offer.</p>
        <div class="priceAndDiscount"> 
            <div class="priceContainer">
                <p class="price"> $125.00</p>
                <p class="discount">50%</p>
            </div>
            <p class="previousPrice">$250.00</p>
            <div class="buttonContainer">
                <el-input-number class="custom-class" v-model="num" :min="1" :max="10" @change="handleChange" size="large"></el-input-number>
                <button @click="addToCart" class="addToCartBtn">
                <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg"><path d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z" fill="#69707D" fill-rule="nonzero"/></svg>
                Add To Cart
                </button>
            </div>
        </div> 
    </article>
</section>
</template>

<style scoped>
    .brand {
        color: var(--darkGrayBlue);
        letter-spacing: .2em;
        font-weight: bold;
        font-size: .8rem;
    }

    .title {
        font-size: 3rem;
        font-weight: bold;
        margin-bottom: .5em;
    }
 
    .textDescrip {
        color: var(--darkGrayBlue);
    }

    .descriptionContainer {
        max-width: 40vw;
    }

    .priceContainer {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        gap: var(--smallSpacing);
    }

    .price {
        font-weight: bold;
        color: black;
        font-size: 2rem;
        margin-bottom: unset;
    }

    .discount {
        padding: .4rem .8rem;
        color: white;
        background-color: black;
        border-radius: 10px;
        margin-bottom: unset;
    }

    .previousPrice {
        color: var(--darkGrayBlue);
        text-decoration: line-through;
    }

    .buttonContainer {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        gap: var(--largeSpacing);
    }

    .addToCartBtn {
        background-color: var(--orange);
        padding: .6em 3em;
        color: var(--darkGrayBlue);
        border-radius: var(--borderRadius);
        border: 2px solid var(--orange);
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 1em;
        font-weight: bold;
        transition: .3s ease-in-out;
    }

    .addToCartBtn:hover {
        background-color: var(--paleOrange);
        border: 2px solid var(--paleOrange);
        transform: scale(105%);
        cursor: pointer;
    }

    .el-input__wrapper {
        color: red;
        size: 10rem;
    }
</style>