<template>
  <div class="question-header">
    <template v-if="question.information">
      <img
        @click="showInfo()"
        class="question-header__info-icon"
        src="../assets/question.png"
      />
      <div
        v-if="appear"
        @click="closeInfo($event)"
        class="question-header__info-text-wrapper"
        :style="{ top: topShift + 'px' }"
      >
        <div class="question-header__info-text">
          <img class="question-header__close-icon" src="../assets/close.png" />
          {{ question.information }}
        </div>
      </div>
    </template>
    <h3 class="question-header__question-text">
      {{ question.checkbox ?? question.question }}
    </h3>
  </div>
</template>

<script>
export default {
  name: "QuestionHeader",
  props: ["question"],
  data() {
    return {
      appear: false,
      topShift: 0,
    };
  },
  methods: {
    showInfo() {
      this.appear = true;
      document.querySelector("body").style.overflow = "hidden";
      this.topShift = window.pageYOffset;
    },

    closeInfo(event) {
      if (
        event.target !== document.querySelector(".question-header__info-text")
      ) {
        this.appear = false;
        document.querySelector("body").style.overflow = "auto";
        event.preventDefault();
      }
    },
  },
};
</script>

<style>
.question-header {
  display: inline-flex;
}

.question-header__question-text {
  margin: 10px 5px;
}

.question-header__info-icon {
  width: 20px;
  height: 20px;
  align-self: center;
}

.question-header__info-icon:hover {
  opacity: 0.5;
  cursor: pointer;
}

.question-header__info-text {
  background: bisque;
  padding: 15px;
  border-radius: 5px;
  position: absolute;
  top: 35vh;
  left: calc(50vw - 150px);
  width: 300px;
  z-index: 3;
}

.question-header__info-text-wrapper {
  width: 100vw;
  position: absolute;
  height: 102%;
  background: #0000003d;
  top: 0;
  left: 0;
}

.question-header__close-icon {
  width: 10px;
  height: 10px;
  position: absolute;
  right: 8px;
  top: 8px;
  cursor: pointer;
}

.question-header__close-icon:hover {
  opacity: 0.5;
}
</style>
