<template>
    <div class="container">
      <h1> SHOP BY CATEGORY </h1>
        <div v-for="(category) in categories" :key="category">
          <book-category :products="getDisplayProducts(category)" :product_category="category" :updateCart="updateCart"></book-category>
        </div>
    </div>
</template>

<script>
import BookCategoryView from '@/components/BookCategoryView.vue'

export default {
  name: 'Home',
  components: {
    'book-category': BookCategoryView
  },
  props: [ 'dataset', 'updateCart'],
  data () {
    return {
      'collections': this.dataset,
      'categories': []
    }
  },
  created () {
    this.categories = this.getCategories()
  },
  methods: {
    getCategories: function () {
      let listedCategories = []
      this.collections.filter((item) => {
        if (!listedCategories.includes(item.genre)) {
          listedCategories.push(item.genre)
        }
      })
      return listedCategories
    },
    getDisplayProducts (category) {
      let productList = this.collections.filter((element) => {
        if (element.genre === category) {
          return element
        }
      })
      return productList.slice(0, 3)
    }
  }
}
</script>

<style scoped>
h1{
  text-align: center;
}
</style>
