<template>
  <div class="container" style="overflow: inherit;">
    <!---->
    <div class="about-button"><i class="material-icons icon-menu">menu</i></div>
    <main>
      <header class="small">
        <h1>Challenge Yourself</h1></header>
      <!---->
      <section v-if='showType==="IN"'>
        <!-- <div class="turnDisplay">
          <h2>Player Two</h2></div> -->
        <div class="question-box">
          <h3 class="ques-title">{{currQuestion.category}}</h3>
          <h2 class="ques-desc">{{currQuestion.question}}</h2>
          <ul>
            <li v-for="(item,index) in currQuestion.option">
              <button @click="alternative(index)" :class="classObject(item)" :disabled="btnDisabled">{{item.name}}</button>
            </li>
            <li v-if="showNextBtn">
              <button @click="nextQuestion()">Next</button>
            </li>
          </ul>
        </div>
        <div>
          <!-- <div class="multi">
            <div class="droplet-container"><i class="droplet incorrect"></i><i class="droplet incorrect"></i><i class="droplet incorrect"></i><i class="droplet correct"></i><i class="droplet incorrect"></i></div>
            <div class="droplet-container"><i class="droplet incorrect"></i><i class="droplet incorrect"></i><i class="droplet correct"></i><i class="droplet incorrect"></i><i class="droplet"></i></div>
          </div> -->
        </div>
        <div>
        </div>
      </section>
      <section v-if='showType==="END"'>
        <div class="question-box">
          <h3 class="ques-title">您的分数是：{{score}}</h3>
          <h2 class="ques-desc">{{tipText}}</h2>
        </div>
      </section>
    </main>
    <el-dialog title="" :visible.sync="dialogFormVisible">
          <h1 class="ques-title">您的分数是：{{score}}</h1>
      <el-button @click="replay" class="dialog-btn" type="primary" plain>New Game</el-button>
      <el-button @click="back" class="dialog-btn" type="primary" plain>Back</el-button>
    </el-dialog>
  </div>
</template>
<script>
import list from '../assets/question.json'

export default {
  name: 'HelloWorld',
  data: function() {
    // body...
    return {
      questionList: list,
      currQuestion: Object.assign({},list[0]),
      score: 0,
      count: 0,
      totalResult: [],
      showType: 'IN',
      showNextBtn: false,
      btnDisabled: false,
      tipText: '',
      dialogFormVisible:false,
      msg: 'Challenge Yourself!'
    }
  },
  methods: {
    alternative(index) {
      let result = 0;

      if (this.checkAnswer(index)) {
        ++this.score
        result = 1;
      } else {
        result = 0;
      }

      this.totalResult.push(result)
      this.showAnswer();

      if (this.count >= this.questionList.length - 1) {
        this.showDialog()
        // this.showType = 'END'
        return
      }
      this.showNextBtn=true;
    },
    classObject: function(item) {
      console.log(item.result)
      if (typeof item.result === 'undefined') {
        return {}
      }
      return {
        'incorrect': !item.result,
        'correct': item.result
      }
    },
    checkAnswer(index) {
      // const ls=this.currQuestion.option
      return index === this.currQuestion.answer
    },
    showAnswer() {
      let result = [],
        ques = this.currQuestion,
        list = this.currQuestion.option
      for (let i in list) {
        let item = {
          name: list[i].name,
          result: Boolean(i == this.currQuestion.answer)
        };
        console.log(i, this.currQuestion.answer, item.result)
        result.push(item)
      }
      this.$set(this.currQuestion, "option", result)
      console.log(this.currQuestion.option)
      // const ls=this.currQuestion.option
      return
    },
    nextQuestion() {
      ++this.count
      this.showNextBtn = false;
      this.currQuestion = this.questionList[this.count]
    },
    showDialog(){
      this.dialogFormVisible = true;

    },
    replay() {
      this.dialogFormVisible = false;
      this.count=0;
      this.score=0;
      this.currQuestion=Object.assign({},this.questionList[0]);
    },
    back() {
      this.dialogFormVisible = false;
      this.count=0;
      this.score=0;
      this.currQuestion=Object.assign({},this.questionList[0]);
      this.$router.push({
        path:'/'
      })
    }
  }
}

</script>
<style>
button.el-dialog__headerbtn{
  width: 22px;
}
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body,
ul {
  margin: 0;
  padding: 0
}

a,
a.link-dark,
a.link-light {
  color: inherit;
  position: relative;
  text-decoration: none;
  transition: all .3s ease
}

a.link-dark:before,
a.link-light:before,
a:before {
  bottom: -2px;
  right: 0;
  content: "";
  position: absolute;
  transform: scale(1);
  transition: all .3s ease;
  width: 100%;
  height: 2px
}

a.link-dark:hover:before,
a.link-light:hover:before,
a:hover:before {
  transform: scale(0)
}

a.link-light:hover {
  color: #4fc3f7
}

a.link-light:before {
  background-color: #f5f5f5
}

a.link-dark:hover {
  color: #f5f5f5
}

a.link-dark:before {
  background-color: #4fc3f7
}

button {
  align-self: center;
  background-color: #f5f5f5;
  border: 2px solid #f5f5f5;
  border-radius: 190px;
  color: #0277bd;
  cursor: pointer;
  font-family: Quicksand, sans-serif;
  font-size: 1.25em;
  margin: .5em 0;
  outline: none;
  padding: 1em;
  transition: all .25s ease;
  max-width: 400px;
  width: 100%
}

button:disabled,
button:disabled:hover {
  cursor: auto;
  pointer-events: none
}

h2 {
  font-weight: 400
}

ul {
  list-style-type: none
}

@media (hover:hover) {
  button:active,
  button:hover {
    background-color: #4fc3f7;
    border: 2px solid #4fc3f7;
    color: #f5f5f5
  }
}

@media (max-width:600px) {
  body {
    font-size: .85em
  }
}

.flex-center-col {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center
}

.fade-enter-active,
.fade-leave-active {
  transition: all .3s ease
}

.fade-enter,
.fade-leave-to {
  opacity: 0
}

.score-high {
  color: #5cdb80
}

.score-low {
  color: #ff5593
}

@keyframes fade-in {
  0% {
    opacity: 0
  }
  to {
    opacity: 1
  }
}

@keyframes open {
  0% {
    max-height: 0;
    opacity: 0;
    margin-bottom: 0
  }
  to {
    max-height: 1000px;
    opacity: 1;
    margin-bottom: 2em
  }
}

@keyframes close {
  0% {
    max-height: 1000px;
    opacity: 1;
    margin-bottom: 2em
  }
  to {
    max-height: 0;
    opacity: 0;
    margin-bottom: 0
  }
}

body {
  background-color: #4481eb;
  background-image: linear-gradient(0deg, #4481eb 0, #04befe);
  background-repeat: no-repeat;
  display: flex;
  font-family: Quicksand, sans-serif;
  height: 100vh;
  justify-content: center;
  text-align: center
}

body,
header {
  color: #f5f5f5
}

header {
  transform: scale(1)
}

h1,
p {
  margin: 0
}

main {
  animation: fade-in 1.5s ease;
  flex-direction: column;
  justify-content: flex-start;
  height: 100%
}

.about-button,
main {
  align-items: center;
  display: flex
}

.about-button {
  background-color: #0277bd;
  border: 2px solid #4fc3f7;
  border-radius: 100%;
  cursor: pointer;
  justify-content: center;
  position: fixed;
  right: .5em;
  top: .25em;
  width: 40px;
  height: 40px;
  z-index: 1000
}

.container {
  width: 100%
}

.icon-close,
.icon-menu {
  transition: all .3s ease
}

.icon-close:hover,
.icon-menu:hover {
  color: #4fc3f7
}

.grow {
  animation: grow .5s ease forwards
}

.small {
  animation: squeeze .5s ease forwards
}

@keyframes grow {
  0% {
    transform: scale(.66);
    padding: .25em 0
  }
  to {
    transform: scale(1);
    padding: 1em
  }
}

@keyframes squeeze {
  0% {
    transform: scale(1);
    padding: 1em
  }
  to {
    transform: scale(.66);
    padding: .5em 0
  }
}

.expand-enter-active {
  animation: open .75s ease forwards
}

.expand-leave-active {
  animation: close .5s ease forwards
}

section {
  max-width: 600px;
  position: relative;
}

div.question-box {
  background-color: #0277bd;
  border-radius: 25px;
  margin-bottom: 2em;
  padding: 1em 1em 2.5em;
  min-width: 320px;
}

.ques-title {
  color: #4fc3f7;
}

.ques-desc {
  color: #fff;
}

button:disabled,
button:disabled:hover {
  cursor: auto;
  pointer-events: none;
}

.incorrect {
  background-color: #ff5593;
  border: 2px solid #ff5593;
  color: #f5f5f5;
}

.correct {
  background-color: #5cdb80;
  border: 2px solid #5cdb80;
  color: #f5f5f5;
}

.el-button.dialog-btn{
  margin-left: 0;
}


/*底部按钮*/

.multi {
  display: flex;
  justify-content: space-around;
}

.droplet-container {
  display: flex;
  flex-direction: row;
  margin-bottom: 2em;
}

.droplet {
  background-color: #f5f5f5;
  border-radius: 100%;
  margin: 0 5px;
  width: 10px;
  height: 10px;
}

.droplet-container {
  display: flex;
  flex-direction: row;
  margin-bottom: 2em;
}

</style>
