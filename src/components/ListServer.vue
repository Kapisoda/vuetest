<template>
  <div class="col-xs-12 col-sm-6">
    <ul class="list-group">
      <li
        class="list-group-item" style="cursor: pointer"
        v-for="(server, index) in servers" v-on:click="nesto(index)">
        Server #{{server.id}} - STATUS: {{ server.status }} - {{index}}
      </li>

    </ul>
    nova
    <ul class="list-group">
      <app-server v-for="server in servers" :server="server" :key="server.id">

      </app-server>

    </ul>
  </div>
</template>

<script>
  import Server from './Server.vue'
export default{
  data() {
    return{
      servers: [
        {id: 1, status: 'normal'},
        {id: 2, status: 'great'},
        {id: 3, status: 'bad'},
        {id: 4, status: 'high'},
        {id: 5, status: 'normal'}
      ]
    }
  },
  methods: {
    nesto: function (index){
      this.servers[index].id += 1;
    }
  },
  components: {
    appServer: Server
  }
}
</script>
