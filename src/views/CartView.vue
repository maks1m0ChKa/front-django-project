<script setup>
    import cartMethods from '../utils/cart';
    import { ref, watch } from 'vue';
    import { onMounted } from 'vue';

    const cart = ref([]);

    const fetchCart = () => {
        cart.value = cartMethods.getCart();
    }

    const removeItem = (id) => {
        cartMethods.removeFromCartById(id);
        cart.value = cartMethods.getCart();
    }

    const clearCart = () => {
        cartMethods.clearCart();
        cart.value = cartMethods.getCart();
    }

    onMounted(async () => {
        fetchCart();
    })
</script>

<template>
    <div class="container-fluid d-flex h-100 justify-content-center align-items-center p-0">
        <div v-for="item in cart" :key="item.id">
            <img :src="item.image" :alt="item.title" />
            <h3>{{ item.price }}</h3>
            <h3>{{ item.title }}</h3>
            <button type="button" class="btn btn-primary btn-lg px-4 me-md-2" @click="removeItem(item.id)">Remove</button>
        </div>

        <div v-if="cart.length === 0">
            <h3>Product is empty</h3>
        </div>

        <div v-if="cart.length > 0">
            <h3>Total: {{ cartMethods.getCartTotal() }}</h3>
            <button type="button" class="btn btn-primary btn-lg px-4 me-md-2" @click="clearCart()">Clear Basket</button>
        </div>
    </div>
    <div class="">
        

    </div>
</template>
<style scoped>
body{
    
}
</style>

