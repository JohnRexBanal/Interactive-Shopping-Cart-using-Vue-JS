<template>
    <div class="shopping-cart">
      <h2>Shopping Cart</h2>
      <div v-if="cart.length === 0" class="empty-cart">
        No Items in the cart
      </div>
      <ul v-else>
        <li v-for="(item, index) in cart" :key="index" class="cart-item">
          <span class="item-info">{{ item.name }} - {{ item.quantity }} x ₱{{ item.price }}</span>
          <div class="item-actions">
            <button @click="removeFromCart(index)" class="remove-button">Remove</button>
            <input type="number" v-model="item.quantity" @change="updateQuantity(index, item.quantity)" class="quantity-input">
          </div>
        </li>
      </ul>
      <p v-if="cart.length > 0" class="total-price">Total: ₱{{ calculateTotalPrice }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cart: {
        type: Array,
        required: true
      }
    },
    computed: {
      calculateTotalPrice() {
        return this.cart.reduce((total, item) => total + (item.quantity * item.price), 0);
      }
    },
    methods: {
      removeFromCart(index) {
        this.$emit('remove-from-cart', index);
      },
      updateQuantity(index, quantity) {
        this.$emit('update-quantity', index, quantity);
      }
    }
  };
  </script>
  
  <style scoped>
  .shopping-cart {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 8px;
  }
  
  .empty-cart {
    font-style: italic;
    color: #777;
  }
  
  .cart-item {
    margin-bottom: 10px;
    padding: 10px;
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .item-info {
    flex-grow: 1;
  }
  
  .item-actions {
    display: flex;
    align-items: center;
  }
  
  .remove-button {
    background-color: #ff5555;
    color: white;
    border: none;
    padding: 6px 12px;
    border-radius: 4px;
    cursor: pointer;
    margin-right: 10px;
  }
  
  .quantity-input {
    width: 60px;
    padding: 6px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  .total-price {
    margin-top: 10px;
    font-weight: bold;
  }
  </style>
  