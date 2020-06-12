<template>
  <div>
    <div id="nav">
      <Navigation />
    </div>
    <div class="row">
      <div class="col-1"></div>
      <div class="col-4 content">
        <div class="row">
          <h3 class="col-6">My bar ratings</h3>
          <div class="col-2"></div>
          <div data-app class ="col-3 addbutton">
            <newbarratingmodel></newbarratingmodel>
          </div>
        </div>
        <div class="bar-rating-list" >
          <div v-for="barrating in this.barrating.barRatings" :key="barrating.id"> 
            <barratingcard v-bind:rating="barrating"/>
          </div>
        </div>
      </div>
      <div class="col-2"></div>
      <div class="col-4 content">
        <div class="row">
          <h3 class="col-6">My beer ratings</h3>
          <div class="col-2"></div>
          <div data-app class ="col-3 addbutton">
            <addnewbeerrating></addnewbeerrating>
          </div>
        </div>
        <div class="beer-rating-list">
           <div v-for="beerrating in this.beerrating.beerRatings" :key="beerrating.id"> 
            <beerratingcard v-bind:rating="beerrating"/>
          </div>
        </div>
      </div>
      <div class="col-1"></div>
    </div>
  </div>
</template>

<script>
import "../assets/css/main.css";
import axios from 'axios';
import Navigation from "@/components/Navigation.vue";
import barratingcard from '@/components/rating/barratingcard.vue';
import beerratingcard from '@/components/rating/beerratingcard.vue';
import addnewbeerrating from '@/components/rating/beer/addnewbeerrating.vue';
import newbarratingmodel from '@/components/rating/newbarratingmodel.vue';
export default {
  
  name: "App",
  
  components: {
    Navigation,
    barratingcard,
    beerratingcard,
    newbarratingmodel,
    addnewbeerrating,
  },
  computed:
  {
    barrating(){
      return this.$store.getters.getratingcollection},

    beerrating(){
      return this.$store.getters.getratingcollection
    }
      
  },

 data () {
    return {
    }
  },
  
  mounted()
  {
    axios.get('http://217.101.44.31:8086/api/public/bar/getAllUserRatings/' + this.$store.getters.getUser.id)
    .then(data => (
    this.$store.dispatch('SaveRatingCollection', data.data)));
  },
};
</script>
a
<style>
.content {
  margin-top: 2%;
  word-wrap: break-word;
}

.addbutton {
  text-decoration: underline;
  cursor: pointer;
}

.bar-rating-list {
  margin-top: 1%;
  height: 700px;
  background-image: url('../assets/images/barlogo.webp');
  background-position: center;
}

.beer-rating-list {
  margin-top: 1%;
  height: 700px;
  background-image: url('../assets/images/boozebuddieslogo.webp');
  background-position: center;
}
</style>