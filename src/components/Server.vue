<template>
  <div>
    <li class="list-group-item" style="cursor: pointer" v-on:click="meth">
      {{server.id}} + {{server.status}}
    </li>
  </div>
</template>

<script>

  import { serverBus } from './../main'

  export default {
    props:['server'],
    data(){
      return {

      }
    },
    methods: {
      meth: function (){
        serverBus.$emit('meth', this.server);
      }
    }
  }

</script>
