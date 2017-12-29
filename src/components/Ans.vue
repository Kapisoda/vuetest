<template>
  <div>
    <!--<li class="list-group-item" style="  cursor: pointer;" v-on:click="odabrani(ans.ide, question.rightAnswer)" v-bind:style="classObject">-->
    <li class="list-group-item" style="  cursor: pointer;" v-on:click="saljiArray(ans.id)" v-bind:style="classObject">
      <div >{{ans.answer}} / {{ans.id}} / {{ans.correct}}</div>
    </li>

  </div>
</template>

<script>
export default {
  props: ['ans', 'question'],
  data() {
    return{
      provjera: '',
      arrayTocnih: [],
      odgovor: false,
      classObject: {
          backgroundColor: 'white',
          color: 'black'
        }
    }
  },
  methods: {
    saljiArray(index){

      this.odgovor= !this.odgovor;
      if(this.odgovor==true){this.classObject.backgroundColor = 'rgba(0,255,0,0.3)';}else{this.classObject.backgroundColor = 'white';};
      this.$emit('saljiArray', index, this.odgovor);
    }
  /*  odabrani: function (odg, tocniOdgovor){
      if(this.odgovor==true){
        this.odgovor=false;
        let i = this.arrayTocnih.indexOf(odg);
        this.arrayTocnih.splice(i,1);
        this.classObject.backgroundColor = 'white';
      }else{
        this.odgovor=true;
        this.arrayTocnih.push(odg);
        this.classObject.backgroundColor = 'rgba(0,255,0,0.3)';
      }


},*/



  },


}

</script>
