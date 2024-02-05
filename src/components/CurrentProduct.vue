<template>
  <div class="product">
            <img :src="product.images[imageNumber] " alt="" class="product-img">
            <button @click="changeImg" class="my-btn">See another image</button>
            <div class="product-details">
                <p class="product-title"><span>Название: </span>{{ product.title }}</p>
                <p class="product-descr"><span>Описание: </span>{{ product.description }}</p>
                <p class="product-price"><x>Цена: </x>  <span>{{ Math.round(product.price*((100 - product.discountPercentage)/100)) }}</span>{{ product.price }}$</p>
                <p class="product-stock"><span>В наличии: </span>{{ product.stock }}</p>
            </div>
        </div>
</template>

<script setup>
  import {useProductStore} from '@/store/ProductStore.js';
  import { useRoute } from 'vue-router';
  import {computed} from 'vue'


const store = useProductStore()
const route = useRoute()

var imageNumber = computed(()=>store.imgNumber)


setTimeout(() => {
    store.fetchProducts();
}, 2000);

const product = computed(()=> {
  return store.products.find((item) => item.id === Number(route.params.id))
});

function changeImg(){
    if(store.imgNumber < product.value.images.length - 1){
        store.imgNumber++
    }else{
        store.imgNumber = 0
    }
    console.log(product.value.images[imageNumber])
    imageNumber = computed(()=>store.imgNumber)
}


const productPrice = product.price
console.log(productPrice);

</script>

<style>
.my-btn{
    border: 2px solid orange;
    padding: 10px;
    color: rgb(205, 58, 5);
    font-family: Arial, Helvetica, sans-serif;
    font-size: 12px;
}
  .product-details{
    display: flex;
    flex-direction: column;
    gap: 10px;
}
.product{
    padding: 12px;
    display: flex;
    border-radius: 12px;
    justify-content: space-around;
    align-items: center;
}
.product-img{
    max-width:320px;
    border-radius: 12px;
    object-fit: cover;
    object-position: center;
    margin-bottom: 10px;
}
.product-title{
    font-family: Arial;
    font-size: 16px;
    font-weight: 500;
    line-height: 20px;
    letter-spacing: 0em;
}
.product-title span{
    font-family: Raleway;
    font-weight: 900;
}
.product-descr{
    font-family: Arial;
    font-size: 16px;
    font-weight: 500;
    line-height: 20px;
    letter-spacing: 0em;
}
.product-descr span{
    font-family:Raleway;
    font-weight: 900;
}
.product-details{
    max-width: 180px;
}
.product-price span{
    text-decoration: line-through;
    margin-right: 7px;
    color: gray;
}
.product-price x{

    font-family: Raleway;
    font-weight: 900;
}
.product-stock span{
    font-family: Raleway;
    font-weight: 900;
}
</style>