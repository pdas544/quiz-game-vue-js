<template>
  <div>
    <h1>My Quiz Game</h1>
    <ScoreBoard :playerScore="playerScore" :computerScore="computerScore" />
    <h2 v-html="question"></h2>
    
    <div class="options" >
      <template v-for="(answer,index) in answers" :key="index">
        <input type="radio" 
        :disabled="this.answerSubmitted"
        name="options" 
        id="" 
        :value="answer"
        v-model="chosenAnswer">
        <label v-html="answer"></label>
      </template>

    </div>
    <button class="btn-submit" @click="submitAnswer">Submit</button>
  </div>
  <div v-if="this.answerSubmitted"> 
    <h4 v-if="this.chosenAnswer != this.correctAnswer"> &#160; Sorry, Your answer is incorrect. Correct Answer is {{ this.correctAnswer }} </h4>
    <h4 v-else> &#9989; Your Answer is Correct! </h4>
    <button class="btn-submit" @click="getNewQuestion">Next Question</button>
    
  </div>
  
  
</template>

<script>
import ScoreBoard from './components/ScoreBoard.vue';

export default {
  name: 'App',
  components: {
    ScoreBoard
  },
  methods: {
    submitAnswer() {
      if(!this.chosenAnswer) {
        alert('Please select an answer before submitting.');
        return;
      }else{
        this.answerSubmitted = true;
        if(this.chosenAnswer == this.correctAnswer) {
          this.playerScore++;
          // alert('Correct!');
        }else{
          // alert('Incorrect!');
          this.computerScore++;
        }
      }
      
    },

    getNewQuestion() {
      this.answerSubmitted = false;
      this.chosenAnswer = undefined;
      this.question = undefined;
      this.axios
      .get('https://opentdb.com/api.php?amount=10&category=18')
      .then((response) => {
        // console.log(response.data.results[0]);
        this.question = response.data.results[0].question;
        this.correctAnswer = response.data.results[0].correct_answer;
        this.incorrectAnswer = response.data.results[0].incorrect_answers;
      })
    }
  },


  data() {
    return {
      question: undefined,
      correctAnswer: undefined,
      incorrectAnswer: undefined,
      chosenAnswer: undefined,
      answerSubmitted: false,
      playerScore:0,
      computerScore:0
    }
  },

  computed:{
    answers() { 
      if (!this.incorrectAnswer || !this.correctAnswer) {
        return [];
      }
      var answers = JSON.parse(JSON.stringify(this.incorrectAnswer));

      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswer);
      return answers;
    }
  },


  created() {
    this.getNewQuestion();
    
  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#app div{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 750px;
  margin: 50px auto;
}

#app div h2{
  font-size: 24px;
  margin-top: 20px;
  border: 2px solid blue;
  border-radius: 12px;
  height: 50px;
  width: 100%;
  padding: 10px 12px;
}

#app span{
  color: blue;
}

#app div .options{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 30px;
}

#app.btn-submit{
  padding: 10px 20px;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

</style>
