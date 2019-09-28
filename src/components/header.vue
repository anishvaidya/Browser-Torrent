<template>
  <nav class="navbar is-primary">
      <div class="navbar-brand">
        <a class="navbar-item">BrowserTorrent</a>
        <div class="navbar-burger burger" data-target="navItems" v-on:click="toggleMenu"  :class="{'is-active': navIsActive}">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
      <div class="navbar-menu" id="navItems"  :class="{'is-active': navIsActive}">
        <div class="navbar-start">
          <a class="navbar-item" href="/brotorrent">HOME</a>
          <!-- <a class="navbar-item" href="/mytorrents">MY DOWNLOADS</a> -->
        </div>
      </div>
    </nav>
</template>

<script>
export default {
    name: 'navbar',
    data () {
      return {
        navIsActive: false
      }
    },
    methods: {
      toggleMenu: function () {
        this.navIsActive = !this.navIsActive
      }
    }
  }
</script>

<style scoped>

  .navbar-brand .navbar-item{
    font-size: 30px;
    margin-right: 70px;
  }
  .navbar-start .navbar-item{
    font-size: 20px;
    margin-right: 30px;
  }

</style>
