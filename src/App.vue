<template>
  <div id="app">
    <h1 class="title-heading">Interactive Shopping Cart in Vue JS</h1>
    <h2>Product List</h2>
    <ProductList :products="products" @add-to-cart="addToCart"></ProductList>
    <ShoppingCart :cart="cart" @remove-from-cart="removeFromCart" @update-quantity="updateQuantity"></ShoppingCart>

  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';


export default {
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Sisigsilog', price: 60 },
        { id: 2, name: 'Tapsilog', price: 65 },
        { id: 3, name: 'Sausagesilog', price: 70 },
        { id: 4, name: 'Tapasilog', price: 75 },
        { id: 5, name: 'Liemposilog', price: 120 },
        { id: 6, name: 'Longsilog', price: 60 },
        { id: 7, name: 'Tortasilog', price: 70 },
        { id: 8, name: 'Hamsilog', price: 70 },
        { id: 9, name: 'Dogsilog', price: 70 },
        { id: 10, name: 'Cornsilog', price: 70 },
      ],
      cart: []
    };
  },
  methods:{
    addToCart(product) {
      const cartItem = this.cart.find(item => item.id === product.id);
      if (cartItem) {
        cartItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index, quantity) {
      if (quantity < 1) {
        this.removeFromCart(index);
      } else {
        this.cart[index].quantity = quantity;
      }
    }
  }
};
</script>

<style scoped>
.title-heading {
  text-align: center;
}
</style>