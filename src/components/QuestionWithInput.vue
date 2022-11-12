<template>
  <div class="question">
    <QuestionHeader :question="question" />
    <p class="question__warning warning" v-if="warningAppear">
      {{ question.warning }}
    </p>
    <input class="question__input" @change="onChange($event)" />
  </div>
</template>

<script>
import QuestionHeader from "./QuestionHeader.vue";
export default {
  name: "QuestionWithInput",
  components: {
    QuestionHeader,
  },
  props: ["question", "createJson"],
  data(props) {
    return {
      warningAppear: false,
      checkInput: props.question.checkInput,
      nameJson: props.question.nameJson,
    };
  },
  unmounted() {
    this.createJson(this.nameJson, "");
  },
  methods: {
    onChange(event) {
      this.warningAppear = !this.checkInput(event.target.value);
      this.createJson(this.nameJson, event.target.value);
    },
  },
};
</script>

<style>
.question {
  padding: 10px;
  background: #fffde7;
  border-radius: 5px;
  margin-bottom: 10px;
}

.question__warning {
  font-size: 0.7rem;
  font-weight: 600;
  color: #da0000;
}
</style>
