<template>
  <div>
    <li class="list-group-item"  >
      <div v-show="index === question.id">
      {{question.ask}}

        <!--<div v-for="ques in question.answer" style="border: 0.5px solid black;  cursor: pointer;" v-on:click="odabrani(ques.ide, question.rightAnswer)" v-bind:style="classObject">{{ques.year}}</div>-->

        <appAns v-for="ans in question.answer" :ans="ans" :question="question" :key="ans.ide"></appAns>
      </div>
    </li>
    <button v-if="question.id > 0" v-on:click="prev">
       prev
     </button>
     <button v-on:click="next">
       next
     </button>
  </div>
</template>

<script>
import Ans from './Ans.vue';
export default {
  props: ['question', 'index'],
  components: {
    appAns: Ans
  },
  methods: {
  // Go to next question
  next: function() {
    this.question.id++;
    this.$emit('next', this.question.id);
  },
  // Go to previous question
  prev: function() {
    this.question.id--;
  }
}
}

</script>
