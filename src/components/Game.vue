<script >


import  Score  from "./Score.vue";

export default {
  name:'Game',
  components:{
    Score
  },

  data() {//construction de nos données (proprités de données)
    return {
      question: null,
      incorrectAnswer:null,
      correctAnswer:null ,
      chosenAnswer:null,
      answerSubmitted:false,
      userScore:0,
      computerScore:0
    }
  },

  computed:{//contient le proprités calculées 
    answers(){
      let answers =JSON.parse( JSON.stringify(this.incorrectAnswer));
      answers.splice(Math.round(Math.random() * answers.lenght),0,this.correctAnswer);//position , nombre d'element à enlever, l'ement à ajouter
      return answers;
    }
  },
  
  methods: {
    submit_answer(){
        if(!this.chosenAnswer){
        alert("Please pick one of the options below")
      }else{
        this.answerSubmitted = true;

        if(this.chosenAnswer == this.correctAnswer){
          this.userScore +=1;
        }else{
          this.computerScore +=1;
        }
      
      }
      
      
    },

    getNewQuestion(){//pour éviter la duplication de code on fait appel à cette fonction lors du montage de l'application et lors de l'appele à une nouvelle question

      this.answerSubmitted = false;
      this.chosenAnswer = null;
      this.question= null;

      this.axios
      .get('https://opentdb.com/api.php?amount=1&category=18')
      .then((response) =>{
        this.question = response.data.results[0].question;
        this.incorrectAnswer = response.data.results[0].incorrect_answers;
        this.correctAnswer = response.data.results[0].correct_answer;
        console.log(response.data.results[0]);
      })
    },
    reload(){
      this.userScore = 0;
      this.computerScore = 0
    }
  },
  created() {//Hook; chargement de l'application et remplie des données
  this.getNewQuestion();
}
}
</script>

<template>
  <div>
    <Score :userScore="this.userScore" :computerScore="this.computerScore" />
 
  <template v-if="this.question">

    <h1 v-html="this.question"></h1>

    <template v-for="(answer,index) in this.answers" v-bind:key="index">
    
      <input type="radio"
      
      :disabled="this.answerSubmitted"  
      name="choices" 
      :value="answer"
      v-model="this.chosenAnswer" />

    <label for="choices" v-html="answer"></label><br />
    </template>

    <button 
    v-if="!this.answerSubmitted" 
    class="send" 
    type="button" 
    @click="this.submit_answer()">Valider</button>

    <button
    class="reinitialize" 
    type="button" 
    @click="this.reload()">Réinitialiser</button>
    <section class="result" v-if="this.answerSubmitted">

      <h4 v-if="this.chosenAnswer == this.correctAnswer" 
      v-html="'&#9989; Congratulations the answer ' +this.correctAnswer + ' is correct'">
      </h4>
      
      <h4 v-else
      v-html="'&#10060; I am sorry you pick a wrong answer, the correct answer is '  + this.correctAnswer">
      </h4>
      
     
      <button class="send" type="button" @click="this.getNewQuestion()">Next question
      </button>

    </section>

  </template>

  </div> 
</template>

<style>
h1 {
  font-size: 18px;
}
.reinitialize{
  margin-right: 5px;
}
</style>
