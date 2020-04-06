<template>
  <div>
        <span class="tab"
        :class="{activeTab: selectedTab === tab}"
         v-for="(tab, index) in tabs" 
         :key="index" @click="selectedTab = tab"
         >{{ tab }}</span>
         <div v-show="selectedTab ==='Commentaires'">
         <p v-if="!reviews.length">Il n'y a pas encore des commentaires .</p>
         <ul v-else>
         <li v-for="(review, index) in reviews" :key="index">           <p>{{ review.name }}</p>
           <p>Rating: {{ review.rating }}</p>
           <p>{{ review.review }}</p>
           </li>
         </ul>
         
         </div>
         <productreview v-show="selectedTab === 'Faire un commentaire'"
        ></productreview>
         </div>
</template>

<script>
import productreview from './productreview.vue'

export default {
         name: 'producttabs',
        props: {
        reviews: {
          type: Array,
          required: true
        }
      },
    data() {
      return {
        tabs: ['Commentaires', 'Faire un commentaire'],
        selectedTab: 'Commentaires'
      }
    },
  components: {
    productreview
  }
}
</script>

<style>

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
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