<script setup lang="ts">
import { ref } from "vue";

type QuestionState = "notAnswered" | "answered" | "correct" | "error";
interface Question {
  q: string;
  a: string[];
  correct: number|Number[];
}

const props = defineProps({
  questions: Array<Question>,
});

const currentQuestion = ref(0);
const questionState = ref<QuestionState>("notAnswered");
const chosenAnswer = ref<number|null>(null);
const answers = ref([]);

console.log("Questions: ", props.questions?.length)

const clickAnswerHandler = (index) => {
  chosenAnswer.value = index;
  if (questionState.value !== "answered") {
    questionState.value = "answered";
  }
};

const checkAnswer = () => {
  if (questionState.value === "answered") {
    console.log(props.questions[currentQuestion.value].correct, chosenAnswer.value)
    if (props.questions[currentQuestion.value].correct === chosenAnswer.value) {
      questionState.value = "correct";
    } else {
      questionState.value = "error";
    }
  }
};

const showNextQuestion = () => {
  if (questionState.value !== "notAnswered") {
    currentQuestion.value++;
    questionState.value = "notAnswered";
    chosenAnswer.value = null;
  }
}
</script>

<template>
  <div v-for="(question, index) in props.questions" :key="question.q">
    <div v-if="index === currentQuestion">
      <span>{{ index + 1 }}. {{ question.q }}</span>
      <ul class="question-list">
        <li
          class="flex gap-2 items-baseline"
          v-for="(a, answerIndex) in question.a"
          :key="a"
          @click="clickAnswerHandler(answerIndex)"
          :class="answerIndex === chosenAnswer ? questionState : ''"
        >
          <label class="flex gap-2 items-baseline">
            <input
            type="radio"
            :value="a"
            name="answer"
            />
            <span>{{ a }}</span>
          </label>
        </li>
      </ul>
      <div class="flex gap-2" v-if="questionState !== 'notAnswered'">
        <button
          @click="checkAnswer"
          :class="questionState"
        >Проверить ответ</button>
        <button
          v-if="currentQuestion < (props.questions?.length - 1 || 0)"
          :class="questionState"
          @click="showNextQuestion"
        >Следующий вопрос</button>
      </div>
    </div>
  </div>
  <div v-if="currentQuestion === props.questions?.length">
    Спасибо!
    <button
      @click="currentQuestion = 0"
    >Начать заново</button>
  </div>
</template>

<style scoped>
  button {
    padding: 3px 8px;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
    background-color: #eee;
  }
  button.notAnswered {
    background-color: #ccc;
  }
  ul.question-list {
    margin-block: 1rem;
    list-style-type: none;
    display: flex;
    flex-direction: column;
    align-items: baseline;
    gap: 1rem;
  }
  ul li {
    line-height: 1.5rem;
    padding: 3px 8px;
    border-radius: 6px;
    cursor: pointer;
    border-width: 1px;
    border-style: solid;
    border-color: transparent;
    transition: all 0.7s ease;
  }
  ul li.error {
    /* border-color: red; */
    background-color: rgb(255, 175, 175);
  }
  ul li.correct {
    /* border-color: green; */
    background-color: rgb(176, 251, 114);
  }
  ul li label, ul li input {
    cursor: inherit;
  }
  code {
    background-color: #eee;
    color: aqua;
  }
</style>