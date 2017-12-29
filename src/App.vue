<template>
  <div class="container">
    <app-status></app-status>

    <hr>
<!--
      <div class="row">
        <app-list></app-list>
        <app-details></app-details>
      </div>

    <hr>
    <app-managed></app-managed>
    <hr>
-->
    <!--<app-questions v-for="(question, index) in questions" :question="question" :index="index" :key="question.id"></app-questions>-->






    <div v-for="(question, index) in questions">
      <div v-show="index===questionIndex">
        <p>{{question.ask}}</p>
        <appAns v-for="ans in question.answers" :ans='ans' :question="question" @saljiArray="saljiArray('extra', ...arguments)" :key="ans.id"></appAns>
      </div>
    </div>
    <button v-if="questionIndex > 0" v-on:click="prev">
      prev
    </button>
    <button  v-if="questionIndex < sumIndex" v-on:click="next">
      next
    </button>
    <button v-if="questionIndex == sumIndex" v-on:click="finish">zavrsi</button>
  </div>
</template>

<script>
  import Status from './components/StatusServer.vue'
  import Details from './components/DetailsServer.vue'
  import Managed from './components/ManagedServer.vue'
  import List from './components/ListServer.vue'
  import Question from './components/Questions.vue'
  import Ans from './components/Ans.vue'
  export default{
    data(){
      return {
        brojTocnihOdgovora: 0,
        mapa: new Map(),
        arrayPitanja: [],
        arrayOdgovor: [],
        arrayOdgovori: [],
        questionIndex: 0,
        sumIndex: 0,
        string: '',
          questions: [
            { id: 1,
            ask: 'how many years do you have?',
            answers: [{answer: '4', id: 1, correct: false},
                    {answer: '12', id: 2, correct: false},
                    {answer: '30', id: 3, correct: true},
                    {answer: '40', id: 4, correct: false}],
            rightAnswer: [3] },
            { id: 2,
            ask: 'kolki ti je?',
            answers: [{answer:'3cm', id: 5, correct: false},
                    {answer:'4cm', id: 6, correct: true},
                    {answer:'2cm', id: 7, correct: false},
                    {answer:'2,5cm', id: 8, correct: true}],
            rightAnswer: [4,2] },
            { id: 3,
            ask: 'kolki ti je IQ?',
            answers: [{answer:'10', id: 9, correct: true},
                    {answer:'20', id: 10, correct: false},
                    {answer:'15', id: 11, correct: false},
                    {answer:'12', id: 12, correct: false}],
            rightAnswer: [1] },
            { id: 4,
            ask: 'kolko voliš papati?',
            answers: [{answer:'puno', id: 13, correct: true},
                    {answer:'jako puno', id: 14, correct: true},
                    {answer:'najviše', id: 15, correct: false},
                    {answer:'nom nom nom nooooom', id: 16, correct: false}],
            rightAnswer: [2,1] },
            { id: 5,
            ask: 'kolko voliš papati?',
            answers: [{answer:'puno', id: 17, correct: true},
                    {answer:'jako puno', id: 18, correct: true},
                    {answer:'najviše', id: 19, correct: false},
                    {answer:'nom nom nom nooooom', id: 20, correct: false}],
            rightAnswer: [2,1] }
          ]
      }
    },
    created() {
    this.sumIndex=this.questions.length-1;
  },
    methods: {
      saljiArray(extra, index, bool){
        //alert(this.questionIndex+'  '+index+'  '+bool);

          if (bool==true){

            this.arrayOdgovor.push([index, this.questions[this.questionIndex].id]);

          }else{
            for(var k = 0; k < this.arrayOdgovor.length; k++){
                if(this.arrayOdgovor[k][0] == index && this.arrayOdgovor[k][1] == this.questions[this.questionIndex].id){
                  this.arrayOdgovor.splice(k, 1);

                }
                }
          }
          this.arrayOdgovor.sort();

      },
      finish(){
        let arOdgovori1 = [];
        let arOdgovori2 = [];
        let arTocniOdgovori = [];

        for(let i =0; i<this.questions.length; i++){
          for(let j=0; j<this.questions[i].answers.length; j++){
            if(this.questions[i].answers[j].correct==true){
              arTocniOdgovori.push([this.questions[i].answers[j].id, i+1]);
            }
          }
        }
        this.mapa = new Map(this.arrayOdgovor);
        var mapa2 = new Map(arTocniOdgovori);
        for(let i=1; i<this.questions.length+1; i++){
          this.mapa.forEach(function(value, key) {
            if(value==i){
              arOdgovori1.push(key)
            }
          });
          arOdgovori1.sort();
          mapa2.forEach(function(value, key) {
            if(value==i){
              arOdgovori2.push(key)
            }
          });
          arOdgovori2.sort();

          var bool;
          bool=this.equal(arOdgovori1,arOdgovori2);
          if (bool == true){
            this.brojTocnihOdgovora++;
          }
          arOdgovori1=[];
          arOdgovori2=[];
        }
        alert('broj tocnih odgovora: '+this.brojTocnihOdgovora+'/'+this.questions.length);
        this.brojTocnihOdgovora=0;
        arTocniOdgovori = [];


      },
      equal(arrayPrvi, arrayDrugi){
        if (!arrayPrvi)
        return false;

    // compare lengths - can save a lot of time
          if (arrayDrugi.length != arrayPrvi.length)
              return false;

          for (var i = 0, l=arrayDrugi.length; i < l; i++) {
        // Check if we have nested arrays
          if (arrayDrugi[i] instanceof Array && arrayPrvi[i] instanceof Array) {
            // recurse into the nested arrays
            if (!arrayDrugi[i].equals(arrayPrvi[i]))
                return false;
              }
              else if (arrayDrugi[i] != arrayPrvi[i]) {
            // Warning - two different object instances will never be equal: {x:20} != {x:20}
              return false;
            }
          }
          return true;
      },
    // Go to next question
    next: function() {
      this.questionIndex++;
    },
    // Go to previous question
    prev: function() {
      this.questionIndex--;
    }
    },
    components: {
      appStatus: Status,
      appDetails: Details,
      appManaged: Managed,
      appList: List,
      appQuestions: Question,
      appAns: Ans
    }
  }
</script>

<style>

</style>
