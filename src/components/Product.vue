<template>
  <div
    class="product"
    @click.stop="handleClick"
    :style="this.product.images.length > 0 && 'cursor: pointer'"
  >
    <div
      class="product-thumbnail"
      :style="{ backgroundImage: `url(${this.product.hero.href})` }"
    >
      <h2 class="product-name">{{ this.product.name.toUpperCase() }}</h2>
      <h3 v-if="this.product.price" class="product-price">
        <span class="regular-price">${{ this.product.price.regular }}</span>
        <span class="selling-price">${{ this.product.price.selling }}</span>
      </h3>
      <h3 v-else-if="this.product.priceRange" class="product-price">
        <div class="regular-price">
          ${{ this.product.priceRange.regular.low }} - ${{
            this.product.priceRange.regular.high
          }}
        </div>
        <div class="selling-price">
          ${{ this.product.priceRange.selling.low }} - ${{
            this.product.priceRange.selling.high
          }}
        </div>
      </h3>
    </div>
    <ImageCarousel
      v-if="this.product.images.length > 0 && showCarousel"
      :images="this.product.images"
      @close="showCarousel = false"
    />
  </div>
</template>

<script>
import ImageCarousel from "./ImageCarousel";
export default {
  name: "Product",
  components: {
    ImageCarousel
  },
  props: {
    product: Object
  },
  data() {
    return {
      showCarousel: false
    };
  },
  methods: {
    handleClick: function() {
      this.showCarousel = true;
    }
  }
};
</script>

<style scoped>
.product-thumbnail {
  position: relative;
  width: 410px;
  height: 410px;
  background-position: center;
  background-size: cover;
  border-radius: 4px;
  transition: all 0.3s;
  margin-bottom: 40px;
}
.product-thumbnail:hover {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
}
.product-name {
  background-color: rgba(255, 255, 255, 0.5);
  font-size: 13px;
  text-align: left;
  padding: 8px;
  color: #4b4b4b;
}
.product-price {
  padding: 8px;
  background-color: rgba(0, 0, 0, 0.6);
  color: white;
  position: absolute;
  bottom: 50px;
  left: 12px;
  font-size: 16px;
  tex-align: left;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  border-radius: 2px;
}
.regular-price {
  color: #bc3232;
  text-decoration: line-through;
  padding-right: 8px;
}
</style>
