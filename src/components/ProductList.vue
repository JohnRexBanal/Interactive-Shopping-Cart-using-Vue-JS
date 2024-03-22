<template>
    <div>
      <ul class="products-grid">
        <li v-for="product in products" :key="product.id" class="product">
          <div class="card-content">
            {{ product.name }} - ₱{{ product.price }}
            <div>
              <button @click="addToCart(product)">Add to Cart</button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      products: {
        type: Array,
        required: true
      }
    },
    methods: {
      addToCart(product) {
        this.$emit('add-to-cart', product);
      }
    }
  };
  </script>
  
  <style scoped>
  .products-grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 20px; 
    list-style-type: none;
    padding: 0;
  }
  
  .product {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .card-content {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    padding: 16px;
    text-align: center;
    background-color: #f1f1f1;
    height: 120px; 
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  
  button{
    background-color: #4CAF50;
    border: none;
    padding: 10px;
    color: white;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>