<template>
    <div>
  <b-jumbotron>
    <template slot="lead">
        {{currentQuestion.question}}
    </template>
    <hr class="my-4">
        <b-list-group>
        <b-list-group-item v-for="(answer,index) in answers" 
        :key="index"
        @click.prevent="selectedAnswer(index)"
        :class="[
       !answerd && selectedIndex ===index ? 'selected' :  
        answerd && correctIndex === index ? 'correct':
        answerd && selectedIndex ===index && correctIndex !== index ? 'incorrect':''
        ]"

        >

            {{answer}}

            </b-list-group-item>
        </b-list-group>
    <b-button
    @click="submitAnswer" 
    :disabled="answerd || selectedIndex===null"
     variant="primary" >Submit</b-button>
    <b-button @click="next" variant="success" href="#">Next</b-button>
  </b-jumbotron>
</div>
</template>
<script>
import _ from 'lodash'

export default {
    props:{
        currentQuestion:Object,
        next:Function,
        increment:Function
    },
    data(){
        return {
            selectedIndex:null,
            shuffledAnswers:[],
            correctIndex:null,
            answerd:false
            
        }
        
    },
    computed:{
        answers() {
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    },
     watch:{
       currentQuestion:{
           immediate:true,
           handler(){
               this.selectedIndex=null
               this.answerd=false
               this.shuffleAnswers()
           }

       } 
    },
    methods:{
        selectedAnswer(index){
            console.log(this.selectedIndex)
            this.selectedIndex = index

        },
        shuffleAnswers(){
            let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers)
            
            this.correctIndex =  this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
            
        },
        submitAnswer(){
            let isCorrect=false
         if(this.selectedIndex === this.correctIndex){
             isCorrect = true
           
         }
          this.answerd = true
          this.increment(isCorrect)
         
        }

    },

   
   
}
</script>
<style>
.list-group-item:hover{
background-color:#eee;
cursor:pointer
}
.selected{
    background-color:lightblue;
}

.correct{
    background-color:lightgreen;
}
.incorrect{
    background-color:tomato;
}
.list-group{
    margin:10px;
}
.btn{
    margin:5px;
}

</style>
