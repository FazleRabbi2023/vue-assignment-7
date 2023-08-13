<script setup>
import { ref, reactive, onMounted, onBeforeUnmount, nextTick } from 'vue'

let newItem = reactive({ url:''})

const items = ref([
    {
        url:'https://images.unsplash.com/photo-1470770841072-f978cf4d019e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=870&q=80'
    },
    {
        url:'https://images.unsplash.com/photo-1619441207978-3d326c46e2c9?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=869&q=80'
    },
    {
        url:'https://images.unsplash.com/photo-1632681872076-f73c6493414a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=869&q=80'
    },
    {
        url:'https://images.unsplash.com/photo-1558882224-dda166733046?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1469&q=80'
    },
    {
        url:'https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80'
    },
    {
        url:'https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1470&q=80'
    },
])


let carousel = null

onMounted(() =>{
    carousel = new Flickity( '#carousel', {});
})

onBeforeUnmount(() => {
    carousel.destroy()
})

function updateCarousel(){
    items.value.push(newItem)
    console.log(items)
    carousel.destroy()
    nextTick(() =>{
        carousel = new Flickity( '#carousel', {});
    })
}

</script>
<template>
    <div class="mx-auto items mb-16" id="carousel">
        <div class="item" :style="`background-image:url(${item.url})`" v-for="(item, index) in items" :key="index">
        </div>
    </div> 
    <form>
        <div class="flex justify-center">
            <div class="mr-5">
                <input v-model="newItem.url" type="text" id="color-name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required placeholder="Image URL">
            </div>
            <div>
                <button @click.prevent="updateCarousel()" type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add to Carousel</button>
            </div>        
        </div>
    </form>
   
</template>

<style scoped>
.items{
    width: 1000px;
    height:400px;
}

.item{
    width: 1000px;
    height: 400px;
    background-color: gray;
    background-size: cover;
}

@media only screen and (max-width: 600px) {
    .items{
    width: 480px;
    height: 300px;
}
.item{
    width: 480px;
    height: 300px;
    background-color: gray;
    background-size: cover;
}
}
</style>