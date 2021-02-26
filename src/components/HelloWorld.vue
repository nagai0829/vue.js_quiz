<template>
  <div>
    <div v-for="(item, questionIndex) in questions"
      v-bind:key=questionIndex
    >
      <p>{{ item.question }}</p>
      <ul>
        <li v-for="(selection, selectIndex) in item.selections"
          v-bind:key=selectIndex
          @click="clickSelection(questionIndex, selectIndex)"
        >{{ selection.choice }}</li>
      </ul>
    </div>
    <p v-if="answerExistList[questionIndex]">
    {{ getJudgeText(questionIndex) }}
   </p>
  </div>
</template>

<script>
export default {
  data() {
    return{      
      questions: [
        {
          question: "ダチョウの脳みその重さは？",
          selections: [
            {
              "choice": "40g",
              "correct": true
            },
            {
              "choice": "400g",
              "correct": false
            },
            {
              "choice": "1400g",
              "correct": false
            },
          ],
        },
        {
          question: "次のうち生まれたのサイズが一番小さい動物は？",
          selections: [
            {
              "choice": "トイプードル",
              "correct": false
            },
            {
              "choice": "カンガルー",
              "correct": true
            },
            {
              "choice": "キリン",
              "correct": false
            },
          ],
        },
        {
          question: "次のうち本当にある恐竜の名前は？",
          selections: [
            {
              "choice": "ゴジラサウルス",
              "correct": true
            },
            {
              "choice": "デジモンサウルス",
              "correct": false
            },
            {
              "choice": "ポケモンサウルス",
              "correct": false
            },
          ],
        },
      ],
      answerExistList: [],
      count: 0      
    }
  },
  computed: {
      fullScore() {
        return this.questions.length * 10
      },
  methods: {
     getJudgeText(questionIndex) {
        const question = this.questions[questionIndex]
        const answerExist = this.answerExistList[questionIndex]
        const selection = question.selections[answerExist]
        return selection.correct ? '正解' : '不正解'
      },
      clickSelection(questionIndex, selectIndex) {
        if(this.answerExistList[questionIndex]) {
          return
        }
        const clickedQuestion = this.questions[questionIndex]//クリックした質問
        const clickedSelection = clickedQuestion.selections[selectIndex]//クリックした選択肢
        const getClickedCorrect = clickedSelection.correct //クリックした選択肢の回答
        // 回答が正解つまりtrueなら10点加算
        if(getClickedCorrect) {
          this.count += 10
        } else {
          this.count += 0
        }
        // this.$set(this.object, propertyName, value) 👉this.$setについて

        this.$set(this.answerExistList, questionIndex, selectIndex + '')
        
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
