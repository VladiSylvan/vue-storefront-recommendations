<template>
  <div class="product-listing row m0 center-xs start-md" style="width: 100%;">
    <!-- <div
      v-for="(product, key) in products"
      :key="product.id"
      class="col-sm-6 flex"
      :class="['col-md-' + (12/columns), wide(product.sale, product.new, key)]"
    > -->
    <div
      v-for="(product, key) in products"
      :key="product.id"
      class="col-sm-6 flex"
      :class="['col-md-' + (12/columns), wide(product.sale, product.new, key)]"
    >
      <product-tile :product="product" />
    </div>
  </div>
</template>

<script>
import ProductTile from 'theme/components/core/ProductTile'
let lastHero = 0
export default {
  name: 'ProductListing',
  components: {
    ProductTile
  },
  props: {
    products: {
      type: null,
      required: true
    },
    columns: {
      type: [Number, String],
      required: true
    }
  },
  methods: {
    wide (isOnSale, isNew, index) {
      let deltaCondition = index > 0 && ((index - 1) - lastHero) % 2 === 0
      // last image always shouldn't be big, we also need to count from last promoted to check if it will look ok
      let isHero = ((isOnSale === '1' || isNew === '1') && deltaCondition) || (index === this.products.length - 1 && (index - lastHero) % 2 !== 0)
      if (isHero) {
        lastHero = index
      }
      return isHero ? 'col-xs-12' : 'col-xs-6'
    }
  }
}
</script>
