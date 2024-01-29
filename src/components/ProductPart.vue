<template>

    <div class="product-container">
      <div class="product-image">
        <span class="sale" v-if="product?.price?.old_price">Скидка</span>
        <img :src="require(`../assets${product.image.url}`)" alt="">
      </div>
      <div class="product-info">
        <p class="code">{{ product.code }}</p>
        <h2 class="name">{{ product.name }}</h2>
        <div class="price-info">
          <div class="left-part">
            <div class="old-price" v-if="product?.price?.old_price">{{ product.price.old_price }}₽</div>
            <div class="current_price">{{ product?.price?.current_price }}₽</div>
          </div>
          <div class="right-part">
            <button @click="addToStorage('cart')" v-if="!cartExist">
              <img :src="require('../assets/cart.svg')" alt="">
            </button>
            <button @click="addToStorage('cart')" v-else>
              <img :src="require('../assets/checked.svg')" alt="">
            </button>
            <button @click="addToStorage('wish')" v-if="!wishExist">
              <img :src="require('../assets/heart.svg')" alt="">
            </button>
            <button @click="addToStorage('wish')" v-else>
              <img :src="require('../assets/heart_red.svg')" alt="">
            </button>
  
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  
  export default {
    name: "ProductPart",
    data() {
      return {
        cartExist: false,
        wishExist: false,
      }
    },
    props: {
      product: {
        required: true,
        type: Object,
      }
    },
    methods: {
      addToStorage(type = 'cart') {
        const productId = this.product?.id;
        if (!productId) {
          return false;
        }
        const checkLocalStorageExist = this.getStorageData(type + '_' + productId);
        if (checkLocalStorageExist) {
          this.removeStorageItem(type + '_' + productId);
        } else {
          this.setStorageItem(type + '_' + productId, 'true');
        }
        this.checkStorageExist();
      },
      getStorageData(key) {
        return localStorage.getItem(key);
      },
      setStorageItem(key, value) {
        return localStorage.setItem(key, value);
      },
      removeStorageItem(key) {
        return localStorage.removeItem(key);
      },
      checkStorageExist() {
        const cartKey = 'cart';
        const productId = this.product?.id;
        const wishKey = 'wish';
        this.cartExist = this.getStorageData(cartKey + '_' + productId);
        this.wishExist = this.getStorageData(wishKey + '_' + productId);
      }
    },
    mounted() {
      this.checkStorageExist();
    }
  }
  </script>
  
  <style scoped>
  .product-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    row-gap: 32px;
    border: 1px solid #88888824
  }
  
  .product-image {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  
  .sale {
    position: absolute;
    top: 11px;
    left: 0;
    width: 81px;
    height: 24px;
    background-color: #EB5757;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 14px;
    font-weight: 500;
    line-height: 18.20px;
    letter-spacing: 0.14px;
    word-wrap: break-word
  }
  
  .product-info {
    padding: 16px;
  }
  
  .code {
    color: #888888;
    font-size: 10px;
    font-weight: 400;
    line-height: 14px;
    min-height: 14px;
    letter-spacing: 0.20px;
    margin-bottom: 10px;
  }
  
  .name {
    color: black;
    font-size: 16px;
    font-weight: 500;
    line-height: 22.40px;
    letter-spacing: 0.32px;
  }
  
  .price-info {
    font-size: 16px;
    font-weight: 400;
    line-height: 22.40px;
    letter-spacing: 0.32px;
    word-wrap: break-word;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .left-part {
    display: flex;
    gap: 5px
  }
  
  .right-part {
    display: flex;
    gap: 5px
  }
  
  .old-price {
    color: #888888;
    text-decoration: line-through;
  }
  
  .current_price {
    color: black;
    font-weight: 500;
  }
  
  .right-part button {
    background-color: unset;
    border: unset;
  }
  </style>