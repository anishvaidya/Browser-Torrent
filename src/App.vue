<template>
  <div id="app">
    <app-header></app-header>
    <download-form></download-form>
    <app-footer></app-footer>
    <!-- <router-view/> -->
  </div>
</template>

<script>
import header from './components/header.vue';
import footer from './components/footer.vue';
import downloadForm from './components/download-form.vue'

export default {
  name: 'App',
  components: {
    'app-header': header,
    'app-footer': footer,
    'download-form': downloadForm
  }
}
</script>

<style>
#app {

}
</style>
