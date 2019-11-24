 <template>
  <div id="questions">
    <div class="jumbotron">
      <div style="height:50px;">
        <p class="lead">
          <b>{{currentQuestion.question}}</b>
        </p>
      </div>
      <hr class="my-4" />
      <h4>
        <span class="badge badge-primary">Answers :</span>
      </h4>
      <b-list-group>
        <b-list-group-item
          v-for="(answer,index) in shuffledAnswers"
          :key="index"
          @click.prevent="selectAnswer(index)"
          :class="answerClass(index)"
        >
          <ul>
            <li>{{ answer }}</li>
          </ul>
        </b-list-group-item>
      </b-list-group>

      <div class="btn-group">
        <button @click="prev" type="button" class="btn btn-outline-primary">Prev</button>
        <button
          @click="submitAnswer"
          :disabled="selectedIndex === null || answered"
          type="button"
          class="btn btn-outline-success"
        >Submit</button>
        <button @click="next" type="button" class="btn btn-outline-primary">Next</button>
      </div>
    </div>
  </div>
</template>
 
<script>
import _ from "lodash";
export default {
  name: "#questions",
  props: {
    currentQuestion: Object,
    next: Function,
    prev: Function
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswers();
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.currentQuestion.correct_answer
      );
    },
    answerClass(index) {
      let answerClass = "";
      if (!this.answered && this.selectedIndex === index) {
        answerClass = "selected";
      } else if (this.answered && this.correctIndex === index) {
        answerClass = "correct";
      } else if (
        this.answered &&
        this.selectedIndex === index &&
        this.correctIndex !== index
      ) {
        answerClass = "incorrect";
      }
      return answerClass;
    }
  }
};
</script>

<style scoped>
.b-list-group-item:hover {
  background-color: #eeeeee;
  cursor: pointer;
}
.selected {
  background-color: lightblue;
}
.correct {
  background-color: green;
}
.incorrect {
  background-color: red;
}
.btn-group {
  margin-top: 20px;
}
.jumbotron {
  margin-top: 30px;
}
</style> 