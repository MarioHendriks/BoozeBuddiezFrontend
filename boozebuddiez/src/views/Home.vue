<template>
  <div class="container" style="width:100%">
    <div class="home">
      <div class="row">
        <div class="col-sm">
          <div class="textdiv">
            <h1>Booze buddies</h1>
            <h2>The way to remember yesterday</h2>
          </div>
        </div>
      </div>
      <img src="../assets/images/newhome.svg" style="max-width:100%"  alt="booze logo" >

      <!-- Check that the SDK client is not currently loading before accessing is methods -->
      <div v-if="!$auth.loading">
        <!-- show login when not authenticated -->
        <img class="loginbutton" src="../assets/images/googlelogin.webp" @click="login" />
      </div>
    </div>
  </div>
</template>

<script>
// .. imports removed for brevity

export default {
  name: "home",
  components: {},
  methods: {
    // Log the user in
    login() {
      this.$auth.loginWithRedirect();
    },
    // Log the user out
    logout() {
      this.$auth.logout({
        returnTo: window.location.origin
      });
    }
  }
};
</script>

<style>
.loginbutton {
  width: 17%;
  cursor: pointer;
}

@media only screen and (max-width: 800px) {
  .loginbutton {
    width: 100%;
    cursor: pointer;
  }
}

.textdiv {
  width: 55%;
  margin: auto;
  text-align: left;
}
</style>