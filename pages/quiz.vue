<template>
  <div padding>
    <div class="container-app">
      <div class="container-quiz">
        <div class="quiz-header">
          <h2>Quiz</h2>
        </div>
        <div v-for="(element, index) in questions.slice(a, b)" v-show="quiz" :key="index" class="quiz-main">
          <div class="box-question">
            <h3>Question {{ b }}/{{ questions.length }}</h3>
            <p>{{ element.question }}</p>
            <img :src="element.image_src" width="150" alt="">
          </div>
          <div class="box-suggestions">
            <ul>
              <li
                v-for="(item, i) in element.suggestions" :key="i"
                :class="select ? check(item) : ''"
                @click="selectResponse(item)"
              >
                {{ item.suggestion }}
              </li>
            </ul>
          </div>
          <div v-if="score_show" class="box-score">
            <h5>Your score is</h5>
            <h4>{{ score }}/{{ questions.length }}</h4>
          </div>
        </div>
        <div class="quiz-footer">
          <div class="box-button">
            <v-btn color="primary" style="color: white" dark label="Skip" />
            <v-btn dark color="primary" label="Next" @click="nextQuestion()" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data () {
    return {
      questions: [
        {
          question: 'When you have a problem whit someone what are you supposed to do ?',
          suggestions: [
            { suggestion: 'Cry' },
            { suggestion: 'get angry' },
            { suggestion: 'Run away' },
            { suggestion: 'Talk about', correct: true }
          ]
        },
        {
          question: 'When you have a problem which person should you see first?',
          suggestions: [
            { suggestion: 'Myself' },
            { suggestion: 'My sister' },
            { suggestion: 'My mother' },
            { suggestion: 'the person i feel best with', correct: true }
          ]
        },
        {
          question: 'Choose what this image express',
          image:true,
          image_src:'/emotions/man-happy.jpg',
          suggestions:[
            {suggestion: 'Sadness'},
            {suggestion: 'Fear'},
            {suggestion: 'Anger'},
            {suggestion: 'Happiness', correct:true},
          ]
        }
        // {
        //   question: '',
        //   suggestions:[
        //     {suggestion: ''},
        //     {suggestion: ''},
        //     {suggestion: ''},
        //     {suggestion: '', correct:true},
        //   ]
        // },
        // {
        //   question: '',
        //   suggestions:[
        //     {suggestion: ''},
        //     {suggestion: ''},
        //     {suggestion: ''},
        //     {suggestion: '', correct:true},
        //   ]
        // },
        // {
        //   question: '',
        //   suggestions:[
        //     {suggestion: ''},
        //     {suggestion: ''},
        //     {suggestion: ''},
        //     {suggestion: '', correct:true},
        //   ]
        // },
      ],
      a: 0,
      b: 1,
      select: false,
      score: 0,
      quiz: true,
      image:false,
      score_show: false,
      next: false
    }
  },

  methods: {
    selectResponse (e) {
      this.select = true
      this.next = true
      if (e.correct) {
        this.score++
      }
    },

    check (status) {
      if (status.correct) {
        return 'correct'
      } else {
        return 'incorrect'
      }
    },

    nextQuestion () {
      if (this.questions.length - 1 === this.a) {
        this.score_show = true
        this.quiz = false
      } else {
        this.a++
        this.b++
        this.select = false
      }
    }
    // skipQuestion(){
    //   if(this.next) {
    //     return
    //   }
    // }
  }
}
</script>

<style>
  /* *{
    margin: 0 ;
    letter-spacing: 2px;
  } */

  .container-app{
    display: flex;
    width: 100%;
    height: 700px;
    justify-content: center;
  }

  .container-quiz {
    display: flex;
    width: 40%;
    height: 85%;
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto;
    flex-flow: column;
    text-align: center;
    border:  1px solid #e7eae0;
    border-radius: 10px;
    background-color: white;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
  }

  .quiz-header{
    display: flex;
    width: 100%;
    border-bottom: 1px solid #e7eae0;
    justify-content: center;
    align-items: center;
    background-color: #e7eae0;
  }

  .quiz-main{
    display:flex;
    width: 100%;
    height: 90%;
    flex-flow: column;
    margin: auto;
  }

  .quiz-footer{
    display: flex;
    width: 100%;
    height: 10%;
    justify-content: center;
    border-top: 1px solid #e7eae0;
    background-color: #e7eae0;
    border-radius: 0px 0px 10px 10px;
  }

  .box-question {
    margin-top: 20px;
  }

  .box-question p{
    margin-top: 20px;
  }

  .box-suggestions{
    display: flex;
    width: 100%;
    height: 500px;
    justify-content: center;
    margin: auto;
  }

  ul {
    display: flex;
    width: 80%;
    margin: 0;
    padding: 0;
    flex-flow: column;
  }

  ul li {
    list-style: none;
    line-height: 2;
    border: 1px solid #cdd2d2;
    margin-bottom: 20px;
    cursor: pointer;
    border-radius: 10px;
  }

  li:hover{
    background-color: #e7eae0;
  }

  .box-button{
    display: flex;
    width: 100%;
  }

  .box-button button{
    width: 150px;
    height: 35px;
    outline: none;
    border :0;
    border-radius: 15px;
    margin: auto;
  }

   li.correct{
     border: 1px solid rgb(74, 219, 74);
     background-color: rgb(74, 219, 74);
     color: white;
     font-weight: 600;
   }

  li.incorrect{
  border: 1px solid rgb(240, 117, 100);
  background-color: rgb(240, 117, 100);
  color: white;
  font-weight: 600;
   }
</style>
