<template>
    <div class="cart-item-card">
        <div class="header">
            <h3>{{product.name}}</h3>
            <img :src="require('../../assets/img/' + product.image) " alt="image" style="width:30%; aspect-ratio:3/2; object-fit:contain;">
            <h4>В Корзине: {{product.quantity}}</h4>
            <h4>Общая стоимость: {{item_cost.toFixed(2)}}</h4>
        </div>

        <p>{{ description }}...</p>
        <button class="remove" @click="removeFromCart">Удалить</button>
        <button class="add" @click="addToCart">Добавить</button>
    </div>
</template>

<script>
export default {
    props: ['product'],
    methods: {
        addToCart() {
            this.$store.commit('addToCart', this.product)
        },
        removeFromCart() {
            this.$store.commit('removeFromCart', this.product)
        }
    },
    computed: {
        description() {
            return this.product.description.substring(0, 120)
        },
        item_cost() {
            return this.product.price * this.product.quantity
        },
    },
}
</script>

<style lang="scss">
    .cart-item-card {
        width: 90%;
        margin: 5%;
        background-color: white;
        box-shadow: 0 0 5px gray;
        border-radius: 5px;
        padding: 10px;
        text-align: left;

        .header {
            display: flex;
            justify-content: space-around;
        }
    }
    button {
                width: 150px;
                border: none;
                padding: 10px;
                border-radius: 5px;
                margin: 5px;
                cursor: pointer;
            }

            button.remove {
                background: rgb(173, 1, 1);
                color: white;
            }

            button.add {
                background: green;
                color: white;
            }
</style>