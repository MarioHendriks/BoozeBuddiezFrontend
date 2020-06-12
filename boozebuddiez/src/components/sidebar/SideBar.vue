<template>
  <div class="col-xs-12 col-sm-12 col-md-3 col-lg-3 container sideBar ">
      <div  class="row" id="mainContent"> 
          <div class="col-12" v-if="this.chosenSideBar == 0">
              <MapSideBar/>
          </div>
          <div class="col-12" v-else-if="this.chosenSideBar == 1">
              <TimelineSideBar/>
          </div>
          <div class="col-12" v-else>
              <FriendsSideBar/>
          </div>
      </div>
      <div class="row" align="center">
          <div class="col-3"> </div>
          <div class="col-2">
              <div v-bind:class="[chosenSideBar == 0 ? selected : '']" class="button" id="button_map" @click="setSidebar(0)"></div>
          </div>
          <div class="col-2">
              <div v-bind:class="[chosenSideBar == 1 ? selected : '']" class="button" id="button_timeline" @click="setSidebar(1)"></div>
          </div>
          <div class="col-2">
              <div v-bind:class="[chosenSideBar == 2 ? selected : '']" class="button" id="button_friends" @click="setSidebar(2)"></div>
            </div>
      </div>
      
  </div>
</template>

<script>
import MapSideBar from '@/components/sidebar/MapSideBar/MapSideBar.vue'
import FriendsSideBar from '@/components/sidebar/FriendsSideBar/FriendsSideBar.vue'
import TimelineSideBar from '@/components/sidebar/TimelineSideBar/TimelineSideBar.vue'
export default {
    name:"side",
    components:{
        MapSideBar,
        FriendsSideBar,
        TimelineSideBar
    },
    data(){
        return{
            chosenSideBar: 0,
            selected: 'selected'
        }
    },
    methods:{
        setSidebar(number){
            this.chosenSideBar = number
        }
    }
}
</script>

<style>
#mainContent{
    height: 92%;
}
.sideBar{
    background-color: #F9E3B4;    
    border-radius: 20px;
    box-shadow: 2px 2px;
    background-image: url('../../assets/images/boozebuddieslogo.webp');
    background-position: center;
    margin-bottom: 10px;
    min-height: 500px;
}
.button{
    background-color: white;
    height: 50px;
    border-radius: 20px;
    border: black;
    
}
.selected{
    border: 3px solid rgb(230, 158, 4);
}
#button_map{
    background-image: url('../../assets/images/map_icon.webp');
   background-position: center;
    background-size: auto;
}
#button_timeline{
    background-image: url('../../assets/images/timeline_icon.webp');
   background-position: center;
    background-size: auto;
}
#button_friends{
    background-image: url('../../assets/images/friends_icon.webp');
   background-position: center;
    background-size: auto;
}
</style>
