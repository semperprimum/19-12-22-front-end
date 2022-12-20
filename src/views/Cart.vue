<template>
    <div>
        <h1>Ваша Корзина</h1>

        <CartItemCard 
            v-for="product in products" 
            :key="product.id"
            :product="product"   />

        <CartSummaryPaymentCard />
    </div>
</template>

<script>
import CartItemCard from '../components/cart/CartItemCard.vue'
import CartSummaryPaymentCard from '../components/cart/CartSummaryPaymentCard.vue'

export default {
    // name: 'Cart',
    components: {
        CartItemCard, CartSummaryPaymentCard,
    }, 
    computed: {
        products() {
            return this.$store.getters.cartItems
        }
    }
}
</script>