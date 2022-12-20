<template>
  
  <div class="home">
    <h1>Каталог</h1>
    <div class="selected">
    <Select 
    :selected="selected"
    :options="categories"
    @select="sortByCategories"/>
    </div>
    <ProductDescriptionDrawer 
    :product="product"
    :active="active.product_drawer"
    v-on:close-product-drawer="closeProductDrawer"/>

    <div class="product-cards-container">
      <ProductSummaryCard 
        v-for="product in filterredProducts"
        :key="product.id" 
        :product="product"
        v-on:view-product="viewProduct($event)"/>
    </div>
  </div>
</template>

<script>
import items from '../data/items'
import ProductSummaryCard from '../components/products/ProductSummaryCard.vue'
import ProductDescriptionDrawer from '../components/products/ProductDescriptionDrawer'
import Select from '../components/products/Select.vue'

export default {
  name: 'HomeView',
  components: {
    ProductSummaryCard, ProductDescriptionDrawer, Select,
  },
  data() {
    return {
      items: items,
      product: null,
      active: {
        product_drawer: false
      },
      categories: [
        {name: 'Все', value: 'all'},
        {name: 'Обувь', value: 'footwear'},
        {name: 'Куртки', value: 'jackets'},
        {name: 'Футболки', value: 't-shirts'},
        {name: 'Нижнее Белье', value: 'underwear'},
        
      ],
      selected: 'Все',
      sortedProducts: [],
    }
  },
  computed: {
    filterredProducts() {
      if(this.sortedProducts.length) {
        return this.sortedProducts
      } else {
        return this.items
      }
    }
  },
  methods: {
    viewProduct(product) {
      this.product = product
      this.active.product_drawer = true
      console.log(this.product)
    },
    closeProductDrawer() {
      this.active.product_drawer = false
    },
    sortByCategories(category) {
      this.sortedProducts = []
      let vm = this
      this.items.map(function (item) {
        if (item.category === category.name) {
          vm.sortedProducts.push(item)
        }
      })
      this.selected = category.name
    }
  }
}
</script>

<style lang="scss">
.product-cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.selected {
  display: flex;
  justify-content: space-around;
}
  
</style>
