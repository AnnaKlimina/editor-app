<template>
  <div class="question">
    <QuestionHeader :question="question" />
    <input type="checkbox" class="question__checkbox" @click="onClick()" />
  </div>
</template>

<script>
import QuestionHeader from "./QuestionHeader.vue";

export default {
  name: "QuestionWithCheckbox",
  props: ["question", "createJson", "handleHideQuestions"],
  components: {
    QuestionHeader,
  },
  data(props) {
    return {
      value: false,
      nameJson: props.question.nameJson,
      hideQuestions: props.question.hideQuestions,
    };
  },
  methods: {
    onClick() {
      this.value = !this.value;
      this.createJson(this.nameJson, this.value);
      this.handleHideQuestions(this.hideQuestions[Number(this.value)]);
    },
  },
};
</script>

<style scoped></style>
