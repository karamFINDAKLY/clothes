
<template>
   <div class="product">
            <div class="product-image">
                <img v-bind:src="image">
            </div>
            <div class="product-info">
                <h1>{{ title }}</h1>
                <p v-if="inStock">Disponible</p>
                <p v-else>Ce produit n'est pas disponible</p>
                <p> Livraison: {{ Shipping }} </p>
                <ul>
                    <li v-for="detail in details" v-bind:key="detail in details">{{ detail }}</li>
                </ul>
                <div class="color-box" v-for="(variant, index) in variants" :key="variant.variantId"
                    :style="{backgroundColor: variant.variantColor }" @click="updateProduct(index)">
                </div>
                <button v-on:click="addToCart" :disabled="!inStock" :class="{ disabledButton: !inStock}"> Ajouter au panier
                    </button>
                    
            </div>
            <producttabs :reviews="reviews">   </producttabs>

                </div>
</template>

<script>
import producttabs from './producttabs.vue'
import eventBus from '../stroe.js'

export default {
     name: 'product',
       props: {
        premium: {
            type: Boolean,
            required: true
        }
    },
      data() {
          
        return {
            product: 'Chemise',
            brand: 'Nike',
            selectedVariant: 0,
            details: ["80% coton", "20% polyester", "Neuter de genre", "Taille : s", "Prix : 67.99$"],
            variants: [{
                    variantId: 2234,
                    variantColor: "black",
                    variantImage: '../assets/pic5.jpg',
                    variantQuantity: 0
                },
                {
                    variantId: 2235,
                    variantColor: "#A9D0F5",
                    variantImage: '../assets/pic3.jpg',
                    variantQuantity: 1


                }
            ],
            reviews: []

        }
    },
  components: {
    producttabs
  },
    methods: {
        addToCart() {
            this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
        },
        updateProduct(index) {
            this.selectedVariant = index
            console.log(index)
        }
     


    },
    computed: {
        title() {
            return this.brand + ' ' + this.product
        },
        image() {

            return this.variants[this.selectedVariant].variantImage
        },
        inStock(){
            return this.variants[this.selectedVariant].variantQuantity
        },
        Shipping() {
            if (this.premium) {
                return "gratuite"
            }
            return "2.99€"
        }
    },
    mounted(){
        eventBus.$on('review-submitted',productReview =>{
            this.reviews.push(productReview)

        })
    }

}
</script>

<style>

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }
  
  .product-image {
    width: 80%;
  }
  
  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }
  
  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }
  
  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  } 
  
  .disabledButton {
    background-color: #d8d8d8;
  }
  
  .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
  }
  
  input {
    width: 100%;  
    height: 25px;
    margin-bottom: 20px;
  }
  
  textarea {
    width: 100%;
    height: 60px;
  }

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
</style>