<template>
  <div id="app">
    <Header/>
    <b-container class='bv-example.row'>
      <b-row>
        <b-col sm='6' offset='3'>
          <QuestionBox
            v-if='questions.length'
            :currentQuestion="questions[index]"
            :next = "next"
            :selectAnswer="selectAnswer"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>



<script>
import Header from './components/Header'
import QuestionBox from './components/QuestionBox'

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return {
      questions: [],
      index: 0,
      selectedInd: null
    }
  },
  methods:{
    next(){
      this.index++
    },
    selectAnswer(ind){
      console.log(ind);
      this.selectedInd = ind
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10', {method: 'get'})
      .then(res=>{
        return res.json()
        })
        .then(result=>{
          console.log(result);
          this.questions = result.results
          console.log(this.questions)
        })
      
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
