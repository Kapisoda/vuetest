<template>
  <div class="container">
    <app-status></app-status>

    <hr>

      <div class="row">
        <app-list></app-list>
        <app-details></app-details>
      </div>

    <hr>
    <app-managed></app-managed>
  </div>
</template>

<script>
  import Status from './components/StatusServer.vue'
  import Details from './components/DetailsServer.vue'
  import Managed from './components/ManagedServer.vue'
  import List from './components/ListServer.vue'
  export default{
    data(){
      return {

      }
    },
    components: {
      appStatus: Status,
      appDetails: Details,
      appManaged: Managed,
      appList: List
    }
  }
</script>

<style>

</style>
