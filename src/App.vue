<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-12 col-md-8 offset-md-2 col-lg-6 offset-lg-3">
        <app-branding/>
        <event-list/>
      </div>
    </div>

  </div>
</template>

<script>
import AppBranding from "@/components/app-branding";
import EventList from "@/components/event-list";

export default {
  name: 'App',
  components: {
    EventList,
    AppBranding

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
