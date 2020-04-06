
<template>
   <form class="review-form" @submit.prevent="onSubmit">
         <p v-if="errors.length">
      <b>Veuillez corriger l'erreur(s) suivante:</b>
      <ul>
        <li v-for="error in errors" v-bind:key="error in errors">{{ error }}</li>
      </ul>
    </p>
      <p>
        <label for="name">Nom:</label>
        <input id="name" v-model="name" placeholder="Nom">
      </p>
      
      <p>
        <label for="review">Commentaire:</label>      
        <textarea id="review" v-model="review" ></textarea>
      </p>
      
      
      <p>
        <label for="rating">Avis:</label>
        <select id="rating" v-model.number="rating">
          <option>5</option>
          <option>4</option>
          <option>3</option>
          <option>2</option>
          <option>1</option>
        </select>
      </p>
          
      <p>
        <input type="submit" value="Soumettre">  
      </p>    
    
    </form>
</template>

<script>
import eventBus from "../stroe.js"
export default {
    name: 'productreview',
     data() {
        return {
            name: null,
            review: null,
            rating: null,
            errors: []

        }
    },
    methods: {
        onSubmit() {
            if (this.name && this.review && this.rating) {
                let productReview = {
                    name: this.name,
                    review: this.review,
                    rating: this.rating
                }
                eventBus.$emit('review-submitted', productReview)
                this.name = null
                this.review = null
                this.rating = null
            } else {
                if (!this.name) this.errors.push("Nom obligatoire.")
                if (!this.review) this.errors.push("Commentaire obligatoire.")
                if (!this.rating) this.errors.push("Avis obligatoire.")
            }
        },
        
    }

}
</script>

<style>
  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
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
</style>