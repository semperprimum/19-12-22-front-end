<template>
    <div class="cart-item-card">
        <h3>Итого: ${{cart_total.toFixed(2)}}</h3>

        <button class="view-product-button">Оплатить Картой</button>
    </div>
</template>

<script>
export default {
    computed: {
        cart_total() {
            return this.$store.getters.cartTotal
        }
    }
}
</script>