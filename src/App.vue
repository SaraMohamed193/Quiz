<template>
  <div id="app">
    <Header 
    :totalNum="totalNum"
    :correctNum="correctNum"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
           <Question
          v-if="questions.length"
         :currentQuestion="questions[index]" 
         :next="next"
         :increment="increment"/></b-col>
      </b-row>
    </b-container>
   
  </div>
</template>

<script>
import Question from './components/Question.vue'
import Header from './components/Header.vue'

export default {
  name: 'app',
  components: {
    Header,
    Question
  },
  
  data (){
    return {
      questions:[],
      index:0,
      correctNum:0,
      totalNum:0

    }
  },
  methods: {
    next(){
       this.index++
    },
    increment(isCorrect){
      if (isCorrect){
        this.correctNum ++
      }
      this.totalNum ++
    }

  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=22&type=multiple',{
      method:'get'
    })
    .then ((response)=>{
      return response.json()
    })
    .then ((jsonData)=>{
      this.questions=jsonData.results
      console.log(this.questions)
    })
  }

}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
</style>
