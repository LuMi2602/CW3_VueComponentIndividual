<template>
  <div id="app">
    <RootComponent />
  </div>
</template>

<script>
import RootComponent from './components/RootComponent.vue';

export default {
  name: 'App',
  components: {
    RootComponent,
  },
};
</script>

<style>
#app {
  text-align: left;
  padding: 20px;
}
</style>
