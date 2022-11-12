<template>
  <div class="question-block">
    <h2 class="question-block__header">{{ questionBlock.header }}</h2>
    <div class="question-block__wrapper">
      <template
        v-for="(item, index) in questionBlock.questionsArray"
        :key="index"
      >
        <QuestionWithCheckbox
          v-if="!hideQuestionsIndexArray.includes(index) && item.checkbox"
          :question="item"
          :createJson="createJson"
          :handleHideQuestions="
            (indexArray) => {
              this.handleHideQuestions(indexArray);
            }
          "
        />
        <QuestionWithInput
          v-if="
            !hideQuestionsIndexArray.includes(index) &&
            !item.checkbox &&
            !item.options.length
          "
          :question="item"
          :createJson="createJson"
        />
        <QuestionWithOptions
          v-if="!hideQuestionsIndexArray.includes(index) && item.options.length"
          :question="item"
          :createJson="createJson"
          :handleHideQuestions="
            (indexArray) => {
              this.handleHideQuestions(indexArray);
            }
          "
        />
      </template>
    </div>
  </div>
</template>

<script>
import QuestionWithCheckbox from "./QuestionWithCheckbox.vue";
import QuestionWithInput from "./QuestionWithInput.vue";
import QuestionWithOptions from "./QuestionWithOptions.vue";

export default {
  name: "QuestionBlock",
  components: {
    QuestionWithCheckbox,
    QuestionWithInput,
    QuestionWithOptions,
  },
  props: ["questionBlock", "createJson"],
  data() {
    return {
      hideQuestionsIndexArray: [],
    };
  },
  methods: {
    handleHideQuestions(indexArray) {
      this.hideQuestionsIndexArray = indexArray;
    },
  },
};
</script>

<style scoped>
.question-block {
  padding: 20px;
  background: #fce181;
  border: 10px double #fef9c7;
}

.question-block__header {
  border-radius: 3px;
  margin-top: -41px;
  background: #f8f5d7;
  width: fit-content;
  padding: 7px 10px;
  box-shadow: 0px 0px 5px #00000082;
}

@media (max-width: 870px) {
  .question-block {
    margin-bottom: 20px;
  }

  .question-block:last-of-type {
    margin-bottom: 0;
  }
}
</style>
