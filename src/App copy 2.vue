<script setup>
import {ref,reactive,computed} from 'vue';
const questions = reactive([
  {
    question: 'what is vue JS?',
    answer: 1,
    options: [
      'A front end framework',
      'A library',
      'An ice cream maker'
    ],
    selected: null
  },
  {
    question: 'what is Vuex?',
    answer: 2,
    options: [
      'Vue with an x',
      'A cheese selection',
      'State mangement library'
    ],
    selected: null
  },
  {
    question: 'what is vue router used for?',
    answer: 1,
    options: [
      'Walking in space',
      'A croting library for vue Js',
      'Burger sauce',
      'Quixxes'
    ],
    selected: null
  }
])
const quizCompleted = ref(false);
const currentQuestion = ref(0);
const score = computed(()=>{
  let value = 0;
  questions.map(q=>{
    if(q.selected==q.answer){
      value++
    }
  })
  return value
})
const getCurrentQuestion = computed(()=>{
  let question = questions[currentQuestion.value]
  question.index = currentQuestion.value
  return question
}) 
const setAnswear = evt=>{
  questions[currentQuestion.value].selected = evt.target.value
  evt.target.value = null
}
const nexQuestion = ()=>{
  if(currentQuestion.value<questions.length-1){
    currentQuestion.value++
  }else{
    quizCompleted.value = true
  }
}
</script>

<template>
<div class="app">
  <h1>The quiz</h1>
  <section class="quiz" v-if="!quizCompleted">
    <div class="quiz-info">
      <span class="question">{{getCurrentQuestion.question}}</span>
      <span class="score">Score {{score}}/{{questions.length}}</span>
    </div>
    <div class="options">
      <label v-for="(option,index) in getCurrentQuestion.options" :key="index" :class="`option ${
          getCurrentQuestion.selected==index
            ?index == getCurrentQuestion.answer
              ?'correct'
              :'wrong'
            :''
        } ${
          getCurrentQuestion.selected!=null && index != getCurrentQuestion.selected?'disabled':''
        }`">
        <input 
          type="radio" 
          :name="getCurrentQuestion.index" 
          :value="index" 
          :disabled = "getCurrentQuestion.selected!=null"
          @click="setAnswear">
        <span>{{option}}</span>
      </label>
    </div>
    <button
      @click="nexQuestion"
      :disabled="getCurrentQuestion.selected==null"
      >
      {{
        getCurrentQuestion.index == questions.length-1
          ?'Finish'
          :getCurrentQuestion.selected==null
            ? 'select an option'
            : 'next question'
      }}
    </button>
  </section>
  <section v-else>
    <h2>You have finished the quiz!</h2>
    <p>Your score is {{ score }} / {{questions.length}}</p>
  </section>
</div>
</template>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat',sans-serif;
}
body{
  background-color: #271c36;
  color:#fff;
}
.app{
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  min-height: 100vh;
}
h1{
  font-size: 2rem;
  margin-bottom: 2rem;
}
.quiz{
  background-color: #382a4b;
  padding: 1rem;
  width: 100%;
  min-width: 640px;
  border-radius: 0.5rem;
}
.quiz-info{
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.quiz-info .question{
  color: #8f8f8f;
  font-size: 1.25rem;
}
.quiz-info .score{
  color: #fff;
  font-size: 1.25rem;
}
.options{
  margin-bottom: 1rem;
}
.option{
  padding: 1rem;
  display: block;
  background-color: #271c36;
  margin-bottom: 0.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
}
.option:hover {
  background-color: #2d213f;
}
.option.correct {
  background-color: #2cce7d;
}
.option.wrong {
  background-color: #ff5a5f;
}
.option:last-of-type{
  margin-bottom: 0;
}
.option.disabled{
  opacity: .5;
}
.option input{
  display: none;
}
button{
  appearance: none;
  outline: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem 1rem;
  background-color: #2cce7d;
  color: #2d213f;
  font-weight: 700;
  text-transform: uppercase;
  font-size: 1.25rem;
  border-radius: 0.5rem;
}
button:disabled{
  opacity: .5;
}
h2{
  font-size: 2rem;
  margin-bottom: 2rem;
  text-align: center;
}
p{
  color: #8f8f8f;
  font-size: 1.25rem;
  text-align: center;
}
</style>
