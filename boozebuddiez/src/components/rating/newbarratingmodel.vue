<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary" v-bind="attrs" v-on="on">Add new Rating</v-btn>
      </template>
      <v-card style="color:blanchedalmond">
        <v-card-title>
          <span class="headline">New Rating</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6">
                <v-autocomplete :items="this.barnames" label="Bars" v-model="rating.name"></v-autocomplete>
              </v-col>
            </v-row>
          </v-container>
          <v-container>
            <StarRating
              v-bind:increment="0.5"
              v-bind:max-rating="5"
              inactive-color="#000"
              active-color="#cc1166"
              v-model="rating.rating"
            ></StarRating>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
          <v-btn color="blue darken-1" text @click="save">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
import StarRating from 'vue-star-rating'
import axios from 'axios'
export default {
  data: () => ({
    dialog: false,
        Bars: null,
    barnames: [],
    rating: {
      rating: null,
      name: null,
      id: null
    }
  }),
  components: {
    StarRating,
  },
  mounted() {
    this.loadBars();
    },
    methods: {
    loadBars() {
      this.Bars = this.$store.getters.getBarCollection;
      this.$store.getters.getBarCollection.filter(bar =>
        this.barnames.push(bar.name)
      );
    },
    save() {
      this.dialog = false;
      this.rating.id = this.Bars.filter(bar => bar.name == this.rating.name);
      this.rating.id = this.rating.id[0].id;
      this.sendtodb();
    },
    sendtodb() {
      axios.post("http://217.101.44.31:8086/api/public/bar/rateBar", {
        
          objectId: this.rating.id,
          objectRating: this.rating.rating,
          userId: this.$store.getters.getUser.id
        })
          .then(respone => {
          if (respone.status == 200) {
            var bar = {
              userId: this.$store.getters.getUser.id,
              barId: this.rating.id,
              rating: this.rating.rating
            };
            var ratings = this.$store.getters.getratingcollection;
            ratings.barRatings.push(bar);
            this.$store.dispatch("SaveRatingCollection", ratings);
          }
        });
    }
  }
};
</script>

<style>
</style>