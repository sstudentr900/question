<script setup>
import {ref,reactive,computed} from 'vue';
const questions = reactive([
  {
    question: '你幾歲？',
    answer: 1,
    options: [
      '18歲',
      '跟你差3歲左右',
      '我的年齡是秘密',
      '妳猜？',
    ],
    selected: null
  },
  {
    question: '在做什麼的？',
    answer: 1,
    options: [
      '導遊',
      '唯恐天下不亂的工作',
      '你想像不到的工作',
      '我沒在工作',
    ],
    selected: null
  },
  {
    question: '你有房子嗎？',
    answer: 3,
    options: [
      '有阿，在信義區',
      '我租房子的',
      '我還沒有打算帶妳回家',
      '乾你屁事'
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
  // console.log('setAnswear evt',evt.target.value)
  // console.log('setAnswear questions',questions[currentQuestion.value])
  questions[currentQuestion.value].selected = evt.target.value
  evt.target.value = null
  // console.log('setAnswear questions',questions[currentQuestion.value])
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
  <div class="container">
    <section class="main">
      <div class="flex">
        <div class="info">
          <div class="infoTop">
            <div class="logo">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                id="圖層_1"
                data-name="圖層 1"
                viewBox="0 0 75.5 70.02"
              >
                <path d="M660.09 392.74c-.05-.32-1.13-.32-1.69-.3-1 0-1.44.21-1.51.63-.13.73.23 1.24.13 2.05 0 .45-6.72 24.39-6.72 24.39.17 0 2.86-.07 3.62-1.79.94-2.13 2.83-10.45 3.76-14.78s2.5-9.69 2.41-10.2Z" transform="translate(-645.91 -349.49)"/>
                <path d="M720.58 400.52c-.34.67-2.41 3.34-2.83 3.27-.83-.14-.86-.94-.64-1.86.27-1.09 1.32-5.48 1.32-5.48.37-1.59-1-2.52-2-3.23-1.58-1.11-5.11-3.17-4.46-4 .16-.21-.35-.81-.52-.82-.7-.08-1.69 1.06-.31 2.63a16.65 16.65 0 0 0 2.38 2.12l.82.67a76.43 76.43 0 0 1-5.28 8.5c-2 2.57-5.06 4.18-5.9 1.55 0 0-.63-2.33.65-2.55a35.69 35.69 0 0 0 5.23-2.56c1.78-1.24 2-5.18-1.82-5.27-1.33 0-5.33.87-6.49 6.35a10.34 10.34 0 0 0-.14 4.21c-2.23 3.16-3.86 4.38-4.87 2.9-.37-.55.29-2.94.45-3.83.29-1.61.57-2.85.95-4.81l.24-1 1.87-.34c1.22-.22 1.58-1.48.35-1.31-.69.09-1.29.19-1.85.28.45-1.92 1.18-4.13.35-3.86-1.52.5-2.33.43-2.44 1.68a4.5 4.5 0 0 1-.1 1.92c0 .12-.13.39-.24.77-1 .24-2 .53-3.31.89l-1.56.44c.45-1.89 1.13-4 .32-3.76-1.52.5-2.32.44-2.43 1.68a4.7 4.7 0 0 1-.11 1.92c0 .14-.15.48-.29.95a17.2 17.2 0 0 0-3.27 1.53c-.87.56.89 1.42 1.77.86l1-.49c-.24 1.1-.51 2.22-.77 3.25a36.89 36.89 0 0 1-3.14 4.62c-2.06 2.49-6.22 4-7.06 1.41 0 0-.64-2.33.65-2.55a35.69 35.69 0 0 0 5.23-2.56c1.78-1.24 2-5.18-1.83-5.26a6.47 6.47 0 0 0-5.49 3.59 39.8 39.8 0 0 0-4.43.53 7.57 7.57 0 0 0-1.3-1.49 7.18 7.18 0 0 0-4-1.5l.57-.36a10.79 10.79 0 0 0 3.58-3.56 6.14 6.14 0 0 0 .54-4.09 5.32 5.32 0 0 0-3.67-3.9c-1.64-.66-4.89-.5-7.34.06-2.74.62-9.34 3-12 8.49a5.88 5.88 0 0 0-.3 4.82 3.26 3.26 0 0 0 2.15 2c1.24.27 2.57-1.76 1.9-2.2a3.5 3.5 0 0 1-1.18-1.3 4.18 4.18 0 0 1 .27-3.54 11.06 11.06 0 0 1 4-3.73 19.12 19.12 0 0 1 6.31-2.43c4.85-.75 6.18.79 6.74 2.42a4.35 4.35 0 0 1-.63 3.67 12 12 0 0 1-3.83 3.23 7.32 7.32 0 0 0-2.17 1.31 2.77 2.77 0 0 0 .16 2 16 16 0 0 0 2.53-1.4c2.23-.94 3.57-.18 4.43.76a4.21 4.21 0 0 1 .77 1.29c-2.44.4-7.62 2.74-10 6.93-.72 1.29-1.64 3.58.05 5.62 1 1.21 3.31 1.76 5.29 1.27a11.05 11.05 0 0 0 7.93-12 6.83 6.83 0 0 0-.27-1.2c1.06-.19 2.17-.33 3.32-.43a12.83 12.83 0 0 0-.43 1.5c-.34 1.61-1 5.47 1.94 7.11 2.72 1.53 5.93.4 9.42-4.42l.21-.32c-.15 1.81 3.18 4.2 4.38 3.49a13.64 13.64 0 0 0 3.67-3.66c1 1.23 2.84 2.2 3.65 1.72a14.38 14.38 0 0 0 3.92-4 4 4 0 0 0 1.43 1.33c2.72 1.52 5.65.25 8.51-4.54 1-1.64 3.06-5.56 4.18-7.7a1.87 1.87 0 0 1 .67 1.2 17.54 17.54 0 0 1-1.18 3.66c-.92 2.66-.9 3.9-.37 4.66a2.76 2.76 0 0 0 3.81.91 9.85 9.85 0 0 0 3.1-3.91c.14-.6-.58-1.1-.76-.75Zm-16.87-1.77a5.88 5.88 0 0 1 2.67-3.56c.7-.36 1.7-.36 1.7 1.33 0 .76-.3 1.64-3.18 2.75-.73.28-1.35.45-1.19-.52ZM677 404.61a5.89 5.89 0 0 1 2.66-3.56c.7-.36 1.71-.36 1.71 1.33 0 .76-.3 1.65-3.18 2.75-.71.28-1.33.45-1.19-.52Zm-9.25 5.66c-.9 1.83-3 4.84-5.43 5.21a2 2 0 0 1-2.31-2.16c0-4.58 6.39-7.45 8.48-7.95a7.64 7.64 0 0 1-.71 4.9Zm20.63-1.41c-.37-.55.3-2.93.46-3.83.28-1.61.56-2.85.94-4.81 0 0 .1-.4.23-1a25.72 25.72 0 0 1 3.05-1c.77-.21 1.36-.36 1.86-.48-.67 3.24-1.67 6.83-2 8.16a1.6 1.6 0 0 0 0 .49c-2.02 2.84-3.54 3.88-4.51 2.47Z" transform="translate(-645.91 -349.49)"/>
                <path d="M652.41 387.08c3.5-1.09 7.64-6.17 11.21-14.94 1.53-.4 3.13-.76 4.77-1.05-.2 2.79-.38 5.49-.47 7.14-.2 3.76.71 5.65 3.78 5.16 1.26-.2 4.45-2.36 6.6-3.93a3 3 0 0 0 1.28 2.36c1.51.68 3.06-.58 3.63-1.22l-1.42 4.1a19.49 19.49 0 0 0-6.2 3.51c-2.39 2.2-2.51 4.3-2.43 5.16a2.81 2.81 0 0 0 2.3 2.84c1.75.38 5-.1 7.51-7.71 2.93-8.95 5-18.16 5-18.16s.16-1.29-.89-.91c-.66.24-1.11.66-1.42.15a1.7 1.7 0 0 0-2.26-.52c-1.52.6-4.36 2.71-5 8.51-1.62 1.07-4.83 3.19-5.58 3.28-.92.11-1.82.14-1.8-1.89 0-3 .08-5.8.13-8.3 1.59-.22 3.2-.38 4.8-.47a1.33 1.33 0 0 0 1.15-.84l.08-.2a.19.19 0 0 0-.19-.26c-2.05.07-4 .21-5.81.38.09-3.8.19-6.81.23-8.66 0-.61-.36-2.27-1.7-2.21-1.85.08-4.72.36-4.82.79a9.32 9.32 0 0 0 .07 2.88 59.48 59.48 0 0 1-3 8.69c-6 1.44-10.15 3.55-12.63 5.93a12.61 12.61 0 0 0-2.59 3.43 5.63 5.63 0 0 0-.47 4.75c.94 2.47 4.31 2.78 6.14 2.21ZM679 391.6c-.92 1.64-2.37 2.76-3.36 2.26-.55-.27-1-2 .91-4.34 1.31-1.65 4.21-2.86 4.61-3a24.65 24.65 0 0 1-2.16 5.08Zm1.93-14a15.3 15.3 0 0 1 1.21-4.41c.57-1.25 1.24-1.93 2-2a.88.88 0 0 1 1 .82 69.65 69.65 0 0 1-1.8 7 2 2 0 0 1-1.69.78c-.65-.15-.86-.79-.71-2.21Zm-13.75-16.33.67-.17a1 1 0 0 1 1.21 1c-.13 1.65-.35 4.51-.57 7.46-1.45.19-2.84.42-4.14.67a89.82 89.82 0 0 0 2.84-8.98ZM648.94 382c.2-1.43 1.08-3 3.07-4.76 1.73-1.52 5-3.05 9-4.29-3 6.1-6.22 9.83-7.85 10.68-2.45 1.22-4.55.6-4.22-1.63ZM693.29 367c-1.58.62-4.58 2.63-4.71 9.13a3.75 3.75 0 0 0 1 2.88 2.22 2.22 0 0 0 1.92.4c1.15-.25 2.12-2.17 2.12-2.17.1.92.87 1.21 1.79 1.07s2.46-1.18 4.12-2.95a4 4 0 0 0 .09.92 1.35 1.35 0 0 0 1.63 1c1.37-.26 2.87-1.44 4.56-3.66-.25 1.57-.38 2.8-.38 2.8 1.4.17 2-1.25 2.18-1.94.25-1.11 1-6.2 1.09-6.5a8.61 8.61 0 0 1 2.19-2.07.49.49 0 0 1 .74.5 35 35 0 0 1-.75 4.25 12 12 0 0 0-.42 3c0 1.42.87 1.9 2.08 1.47 1.83-.64 3.42-2.8 4.48-4.19.29-.38-.13-1.24-.46-.8a13.58 13.58 0 0 1-3 3c-.19.09-1.17.55-1.13-.5a23.87 23.87 0 0 1 .68-2.81 28.59 28.59 0 0 0 .73-4.26 1.68 1.68 0 0 0-.56-1.48 1.56 1.56 0 0 0-1.43-.16 5.6 5.6 0 0 0-3.07 2.55c.08-1 .3-1.94-.26-2-1.54.43-1.95.3-2.07 1.28-.11.81.49.84.49 1.41a44.67 44.67 0 0 1-.76 4.47v.07c-1.93 2.3-3.63 3.81-4.28 3.62-.26-.08-.28-.43-.17-1.22.21-1.55 1.56-7.88 1.56-7.88s.16-1.13-.87-.89c-1.24.29-1.79.46-1.94 1.07-.22 1.42.49 1.24.41 2.07 0 .46-.87 3.83-1.11 5.13v.14c-1.59 1.69-3.08 2.81-3.66 2.68-.28-.06-.3-.48-.17-1.2.27-1.54 1.43-6.81 1.43-6.81s.16-1.26-.87-.9c-.7.25-1.13.41-1.33 0-.04-.01-.3-1.14-1.89-.52Zm.15 8.68c-.61.92-1.06 1.43-1.79 1.54s-.88-.91-.74-2.35a12.83 12.83 0 0 1 1.06-4c.55-1.24 1.21-1.9 2-2a.86.86 0 0 1 1 .79 48.54 48.54 0 0 1-1.53 6.02ZM702.31 363.61a1.77 1.77 0 0 0 1.07-.57 1.46 1.46 0 0 0 .48-1 1 1 0 0 0-.33-.83 1.16 1.16 0 0 0-.95-.21 1.81 1.81 0 0 0-1.07.58 1.47 1.47 0 0 0-.46 1 1 1 0 0 0 .34.84 1.13 1.13 0 0 0 .92.19Z" transform="translate(-645.91 -349.49)"/>
                <path d="m32.97 7.43 1.03-.2.82-4.62.99-.19.13-.74-3 .56-.14.75.99-.19-.82 4.63z"/>
                <path d="m683.49 354 .34-.07.49 1.94 1.11-.21-.56-1.95a1.13 1.13 0 0 0 .79-.94l.29-1.59c.09-.56-.18-.78-.83-.66l-2.08.39-.94 5.37 1-.19Zm.45-2.53.74-.14h.19c.03 0 0 .08 0 .17l-.23 1.35a.37.37 0 0 1-.09.19.42.42 0 0 1-.21.08l-.74.14Z" transform="translate(-645.91 -349.49)"/>
                <path d="m41.66 5.8 1.03-.19.3-1.73L44.88 0l-1.05.2-1.21 2.89-.28-2.61-1.05.19.67 3.43-.3 1.7zM36.12 15.48l.4-2.28 1.38-.26.13-.71-1.39.26.29-1.64 1.7-.32.13-.75-2.74.52-.94 5.37 1.04-.19z"/>
                <path d="m685.62 364.29.4-1.15 1.23-.23v1.07l1-.19-.25-5.15-1.38.26-2.09 5.58Zm1.58-4.58v2.48l-1 .18Z" transform="translate(-645.91 -349.49)"/>
                <path d="m43.66 14.06 1.03-.19.95-5.38-1.03.2-.95 5.37zM48.98 12.34l-1.5.28L48.3 8l-1.03.19-.95 5.37 2.53-.47.13-.75zM49.38 33.98l.14-.75-2.74.52-.95 5.37 1.04-.19.4-2.28 1.39-.26.12-.71-1.38.26.29-1.64 1.69-.32z"/>
                <path d="m696.77 386.59 1.24-.23v1.07l1-.19-.24-5.15-1.39.26-2.08 5.58 1-.19Zm1.19-3.43v2.48l-1 .18Z" transform="translate(-645.91 -349.49)"/>
                <path d="m55.45 37.32.95-5.37-1.03.19-.95 5.37 1.03-.19zM58.02 31.64l-.94 5.37 2.53-.47.13-.75-1.5.28.81-4.62-1.03.19z"/>
              </svg>
            </div>
            <div class="level">
              <svg
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink"
                x="0px"
                y="0px"
                viewBox="0 0 93 44.8"
                enable-background="new 0 0 93 44.8"
                xml:space="preserve"
                class="w-[220px]"
                data-v-70ac7c=""
                data-v-92de44=""
              >
                <path
                  fill="#FFFFFF"
                  stroke="#000000"
                  stroke-miterlimit="10"
                  d="M92.5,28.7l-21.7,7.2c-4.3,1.3-8.6-1.9-8.6-6.3V11.3l30.2-9.8
                V28.7z"
                ></path>
                <path
                  fill="#FFFFFF"
                  stroke="#000000"
                  stroke-miterlimit="10"
                  d="M53.7,0.8L0.5,16.9v27.2l57.7-17.5c1.6-0.4,4.1-0.6,4.1,1.6v-2.9
                v-1.9V7.1C62.3,2.7,58-0.5,53.7,0.8z"
                ></path>
                <text class="font-teko uppercase" transform="matrix(1 -0.3029 0 1 6.2953 35.6741)" font-size="20.6697px">failure</text>
                <text transform="matrix(1 -0.3029 0 1 69.0404 29.0585)" data-v-70ac7c="">
                  <tspan
                    class="font-teko"
                    x="0"
                    y="0"
                    font-family="'Teko-Regular'"
                    font-size="20.6697px"
                    letter-spacing="1"
                    data-v-70ac7c=""
                  >0</tspan>
                  <tspan
                    class="font-teko font-semibold"
                    x="9.7"
                    y="-0.5"
                    font-family="'Teko-SemiBold'"
                    font-size="9.4879px"
                    data-v-70ac7c=""
                  >/5</tspan>
                </text>
              </svg>
            </div>
          </div>
          <div class="share">
            <div class="item">
              <div class="flex">
                <a href="#">
                  <svg xmlns="http://www.w3.org/2000/svg" id="ae696ae7-afd0-40c3-aa3c-75facf4fee46" viewBox="0 0 29.1 29.1">
                    <path d="M14.6 7.1a7.5 7.5 0 1 0 7.4 7.5 7.5 7.5 0 0 0-7.4-7.5Zm-.1 12.4a5 5 0 1 1 5-5 4.9 4.9 0 0 1-5 5Z"/>
                    <path d="M29.1 8.4A8.3 8.3 0 0 0 20.7 0H8.4A8.3 8.3 0 0 0 0 8.4v12.4a8.3 8.3 0 0 0 8.3 8.3H22a8.2 8.2 0 0 0 7.1-8.3V8.4Zm-2.5 12.3a5.7 5.7 0 0 1-5.9 5.9H8.4a5.7 5.7 0 0 1-5.9-5.9V8.4a5.8 5.8 0 0 1 5.9-5.9h12.3a5.8 5.8 0 0 1 5.9 5.9Z"/>
                    <path d="M22.3 4.9a1.8 1.8 0 1 0 1.8 1.8 1.8 1.8 0 0 0-1.8-1.8Z"/>
                  </svg>
                </a>
              </div>
              <p>MSSP</p>
            </div>
            <div class="item">
              <div class="flex">
                <a href="#">
                  <svg xmlns="http://www.w3.org/2000/svg" id="ae696ae7-afd0-40c3-aa3c-75facf4fee46" viewBox="0 0 29.1 29.1">
                    <path d="M14.6 7.1a7.5 7.5 0 1 0 7.4 7.5 7.5 7.5 0 0 0-7.4-7.5Zm-.1 12.4a5 5 0 1 1 5-5 4.9 4.9 0 0 1-5 5Z"/>
                    <path d="M29.1 8.4A8.3 8.3 0 0 0 20.7 0H8.4A8.3 8.3 0 0 0 0 8.4v12.4a8.3 8.3 0 0 0 8.3 8.3H22a8.2 8.2 0 0 0 7.1-8.3V8.4Zm-2.5 12.3a5.7 5.7 0 0 1-5.9 5.9H8.4a5.7 5.7 0 0 1-5.9-5.9V8.4a5.8 5.8 0 0 1 5.9-5.9h12.3a5.8 5.8 0 0 1 5.9 5.9Z"/>
                    <path d="M22.3 4.9a1.8 1.8 0 1 0 1.8 1.8 1.8 1.8 0 0 0-1.8-1.8Z"/>
                  </svg>
                </a>
                <a href="#">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    id="e3c23a84-5d1a-4b45-bf04-80df42b9cdfb"
                    data-name="圖層 1"
                    viewBox="0 0 28.7 29.1"
                  >
                    <path d="M21.9 0H6.8A6.7 6.7 0 0 0 0 6.8v15.5a6.7 6.7 0 0 0 6.8 6.8h8V18.6c0-.3 0-.4-.3-.3h-1.8v-4.4h2.1v-.5a24.5 24.5 0 0 1 .2-2.7 3.8 3.8 0 0 1 3.6-3.3c1.3-.1 2.7 0 4.1 0v3.7h-2.3c-.7 0-1 .3-1 1a9.7 9.7 0 0 0-.1 1.7h3.5c-.1 1.5-.3 2.9-.4 4.4h-2.9c-.2 0-.3 0-.3.3v10.6h2.7a6.7 6.7 0 0 0 6.8-6.8V6.8A6.7 6.7 0 0 0 21.9 0Z"/>
                  </svg>
                </a>
              </div>
              <p>MSSP</p>
            </div>
          </div>
        </div>
        <div class="enterName">
          <label>你的名字是?</label>
          <input type="text">
          <button>START</button>
        </div>
      </div>
      <div class="title">
        <h1>歡迎進入，</h1>
        <h1>廢物測試，你能答對幾題......</h1>
      </div>
    </section>
    <section class="ad">
      <ul>
        <li>廢物測試，測試你有多廢</li>
        <li>廢物測試，測試你有多廢</li>
        <li>廢物測試，測試你有多廢</li>
        <li>廢物測試，測試你有多廢</li>
        <li>廢物測試，測試你有多廢</li>
        <li>廢物測試，測試你有多廢</li>
      </ul>
    </section>
  </div>
</template>
<style lang="sass">
  @keyframes move 
    0%
      transform: translateX(0)
    100%
      transform: translateX(-100%)
  *
    box-sizing: border-box
  body,html
    padding: 0 
    margin: 0 
    font-family: MyriadPro,Noto Sans TC,Noto Sans JP,ui-sans-serif,system-ui,-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,Noto Sans,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji
  p
    margin: 0
  [class^=flex]
    display: flex
  ul
    list-style: none
    margin: 0
    padding: 0
  .container
    max-width: 1280px
    width: 100%
    margin: auto  
    padding: 0 40px 40px
  .title
    position: absolute
    top: 0
    right: 0
    writing-mode: vertical-rl
    transform: translate(-0.5rem,2.5rem)
    h1
      background: #fff
      border: 2px solid rgb(0 0 0)
      margin: 0
      padding: 1.5rem 1.2rem 2.5rem
      font-size: 1.875rem
      line-height: 1.6rem
      letter-spacing: .3rem
      text-orientation: upright 
      border-radius: 12px
    h1:nth-child(1)
      display: inline-block
      border-left: none
      border-top-left-radius: 0
      border-bottom-left-radius: 0
    h1:nth-child(2)  
      border-top-right-radius: 0  
  .info
    width: 245px
    border-right: 1px solid #000
    display: flex
    flex-direction: column
    justify-content: space-between
    .infoTop
      transform: translate(-15px, -130px)
    .logo
      svg
        width: 270px  
    .level
      margin-top: 30px
      svg
        width: 220px
        font-family: Teko-Regular
    .share
      padding: 0 36px 36px
      .flex
        margin-bottom: 8px
      .item+.item
        margin-top: 16px  
      a+a
        margin-left: 12px
      svg
        width:24px
        height: 24px
  .enterName
    flex:  1 1
    display: flex
    align-items: center
    justify-content: center
    flex-direction: column
    label
      font-size: 1.875rem
      line-height: 2.25rem
      margin-bottom: 1.5rem
    input
      max-width: 32rem
      width: 100%
      margin-bottom: 2rem
      border: none
      border-bottom: 1px solid rgb(0, 0, 0)
    button
      font-size: 1.25rem
      line-height: 1.75rem
      padding: 0.5rem 2rem
      border-width: 3px
      border-radius: 0.75rem
      background-color: rgb(0 249 134)
  .main
    padding-top: 160px
    position: relative
    >.flex
      border: 1px solid #000
      border-radius: 8px
      min-height: 680px
  .ad    
    padding-top: 0.5rem
    padding-bottom: 0.5rem
    border: 1px solid #000
    margin: 2rem 0 1.5rem
    overflow: hidden
    font-size: 20px
    letter-spacing: 2px
    font-weight: bold
    ul
      display: flex
      overflow: hidden
      width: 1530px
      li
        padding: 0 0 0 12px 
        animation: move 2s infinite linear
</style>
