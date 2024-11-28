<script setup>
import { ref } from 'vue';
import image1 from '@/assets/images/image-product-1.jpg';
import image2 from '@/assets/images/image-product-2.jpg';
import image3 from '@/assets/images/image-product-3.jpg';
import image4 from '@/assets/images/image-product-4.jpg';

//Saves images in array
const images = [image1, image2, image3, image4]
//Initially set to the first image in the 'images' array (images[0])
const selectedImage = ref(images[0])
//sets modal to false by default so its hidden. 
let showModal = ref(false)

// functions
//takes 'image' as a parameter and updates the 'selectedImage' reference to the new image
let selectImage = (image) => {
    selectedImage.value = image
}

//modal open and close
let showModalConfirm = () => {
    showModal.value = true
}
</script>

<template>
    <section class="container"> 
        <transition name="fade" mode="out-in">
            <img @click="showModalConfirm"
                v-if="selectedImage" 
                :src="selectedImage" 
                alt="Selected Product" 
                class="ProductImage chosenImage" 
                :key="selectedImage" 
            />
        </transition>
            <div class="nonSelectedImages">
                <img
                    v-for="(image, index) in images"
                    :key="index"
                    :src="image"
                    alt="Thumbnail"
                    @click="selectImage(image)"
                    :class="{ active: image === selectedImage.value }"
                />
            </div>

        <transition name="fade">
            <div v-if="showModal" class="modalBackdrop" @click="showModal = false">
                <div class="modalContent">
                    <img
                    v-if="selectedImage" 
                    :src="selectedImage" 
                    alt="Selected Product" 
                    class="ProductImage chosenImage modalImage" 
                    :key="selectedImage" 
                />
                    <div class="modalCloseX">
                    <img @click="showModal = false" src="../assets/images/icon-close.svg" alt="">
                    </div>
                </div>
            </div>
        </transition>
    </section>
</template>

<style scoped>
    .modalContent .modalImage{
        max-height: 70vh;
        border-radius: var(--borderRadius);
        position: relative;
        bottom: -130px;
        left: 33%;
        z-index: 2;
    }

    .modalCloseX img {
        position: absolute;
        top: 150px;
        right: 420px;
        transition: .2s ease-in-out;
        z-index: 3;
    }

    .modalCloseX img:hover {
        transform: scale(130%);
        cursor: pointer;
    }

     .modalBackdrop {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.659); 
        box-shadow: 0 0 150px rgba(0, 0, 0, 0.7);
        z-index: 4;
    }

    .fade-enter-active, .fade-leave-active {
        transition:  0.3s ease-in-out;
    }

    .fade-enter, .fade-leave-to {
        opacity: 0;
    }

    .chosenImage {
        transition:  0.3s ease-in-out;
    }
    
    .container {
        height: 60vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .chosenImage {
        border-radius: 20px;
        height: 100%;
        max-width: 100%;
    }

    .nonSelectedImages {
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: var(--smallSpacing);
        margin: 2rem 0;
    }

    .nonSelectedImages img {
        border-radius: 15px;
        height: 12vh;
        object-fit: cover;
        transition: .3s ease-in-out;
        border: 2px solid rgba(0, 0, 0, 0);
    }

    .nonSelectedImages img:hover {
        border: 2px solid var(--orange);
        transform: scale(105%);
        cursor: pointer;
    }

    .chosenImage:hover {
        cursor: pointer;
        transform: scale(102%);
    }
</style>
