<template>
  <div>
  <div class="col-xs-12">
      <p>{{server.id}} | {{server.status}}</p>
    <input type="text" v-on:keydown.enter="statusChange">
    <button v-on:click="change">button</button>
    </div>
  </div>
</template>

<script>
  import {serverBus} from './../main'
  export default{
    data(){
      return {
        server: null
      }
    },
    methods: {
      change: function() {
        this.server.status= 'normal';
      },
      statusChange: function(event) {
        this.server.status = event.target.value;
      }
    },
    created(){
      serverBus.$on('meth', (server) => {
        this.server=server;
      });
    }
  }

</script>

<style scoped>


</style>
