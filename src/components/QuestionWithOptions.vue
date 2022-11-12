<template>
  <div class="question">
    <QuestionHeader :question="question" />
    <div class="question__options-container">
      <p
        class="question__option-text"
        v-for="(option, index) in question.options"
        v-bind:key="index"
      >
        <input
          type="radio"
          class="question__option"
          @click="onClick($event)"
          :data-index="index"
        />
        {{ option }}
      </p>
    </div>
  </div>
</template>

<script>
import QuestionHeader from "./QuestionHeader.vue";

export default {
  name: "QuestionWithOptions",
  props: ["question", "createJson", "handleHideQuestions"],
  components: {
    QuestionHeader,
  },
  data(props) {
    return {
      value: null,
      nameJson: props.question.nameJson,
      hideQuestions: props.question.hideQuestions,
    };
  },
  methods: {
    onClick(event) {
      this.value = event.target.closest(".question__option-text").textContent;
      let checkedOption = event.target
        .closest(".question__options-container")
        .querySelectorAll("input[type=radio]:checked");
      event.target.checked = true;
      for (let element of checkedOption) {
        if (element !== event.target) {
          element.checked = false;
        }
      }
      if (this.hideQuestions) {
        this.handleHideQuestions(
          this.hideQuestions[event.target.dataset.index]
        );
      }
      this.createJson(this.nameJson, this.value);
    },
  },
};
</script>

<style scoped></style>
