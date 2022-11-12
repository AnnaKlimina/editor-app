<template>
  <div class="editor-main">
    <QuestionBlock
      v-for="(block, index) in editorQuestions"
      :key="index"
      :questionBlock="block"
      :createJson="
        (propName, value) => {
          createJson(propName, value);
        }
      "
    />
  </div>
  <div class="editor-main__button-container">
    <p class="editor-main__warning" v-if="warningAppear">
      Пожалуйста, проверьте введённые данные
    </p>
    <CreateButton @show-json="showJson($event)" />
  </div>
  <CodeElement :jsonShown="jsonShown" />
</template>

<script>
import QuestionBlock from "./QuestionBlock.vue";
import CreateButton from "./CreateButton.vue";
import CodeElement from "./CodeElement.vue";

export default {
  name: "EditorMain",
  components: {
    QuestionBlock,
    CreateButton,
    CodeElement,
  },
  data() {
    return {
      editorQuestions: data,
      warningAppear: false,
      jsonResult: {},
      jsonShown: "",
    };
  },
  methods: {
    showJson() {
      if (document.querySelectorAll("[class~='warning']").length) {
        this.warningAppear = true;
      } else {
        this.warningAppear = false;
        this.jsonShown = Object.keys(this.jsonResult).length
          ? JSON.parse(JSON.stringify(this.jsonResult), (key, value) => {
              if (value === "") return undefined;
              if (isNaN(value) || typeof value === "boolean") {
                return value;
              } else {
                return Number(value);
              }
            })
          : "";
      }
    },
    createJson(propName, value) {
      this.jsonResult[propName] = value;
    },
  },
};

let data = [
  {
    header: "Структура Нейросети",
    questionsArray: [
      {
        question: "Количество скрытых слоев:",
        nameJson: "number_of_hidden_layers",
        options: [0, 1, 2],
        hideQuestions: [[1, 2], [2], []],
        defaultValue: 1,
      },
      {
        question: "Количество нейронов в первом скрытом слое:",
        nameJson: "number_of_neurons_in_first_layer",
        options: [],
        defaultValue: 10,
        checkInput: isNaturalNumber,
        warning: "Пожалуйста, проверьте свой ввод. Необходимо целое число >= 1",
      },
      {
        question: "Количество нейронов во втором скрытом слое:",
        nameJson: "number_of_neurons_in_second_layer",
        options: [],
        defaultValue: 10,
        checkInput: isNaturalNumber,
        warning: "Пожалуйста, проверьте свой ввод. Необходимо целое число >= 1",
      },
    ],
  },
  {
    header: "Параметры обучения",
    questionsArray: [
      {
        question: "Количество рестартов:",
        nameJson: "number_of_restarts",
        options: [],
        defaultValue: 10,
        checkInput: isNaturalNumber,
        warning: "Пожалуйста, проверьте свой ввод. Необходимо целое число >= 1",
        information:
          "Число попыток обучения Нейросети (на одном и том же наборе), выполняемых из случайных начальных значений весов. По завершении всех рестартов выбирается сеть, которая обеспечивает наименьшую среднеквадратическую ошибку на обучающем множестве. Целое число >= 1.",
      },
      {
        question: "Степень регуляризации (в %):",
        nameJson: "degree_of_regularization_(%)",
        options: [0, 20, 40, 60, 80, 100],
        information:
          "Степень зависимости весов сети друг от друга. Чем больше эта зависимость, тем сильнее будет влияние одного входного параметра на другие. Регуляризация позволяет снизить эффективное число степеней свободы модели, избежав тем самым переобучения.",
        defaultValue: 40,
      },
      {
        question: "",
        nameJson: "continue_training_flag",
        options: [],
        hideQuestions: [[], [0]],
        defaultValue: null,
        checkbox: "Продолжить обучение",
        information:
          "Установка данного флага позволяет начать переобучение модели не со случайных значений весов Нейросети, а с полученных при последнем обучении. При этом параметр Количество рестартов игнорируется.",
      },
    ],
  },
  {
    header: "Критерии останова",
    questionsArray: [
      {
        question: "Порог минимального изменения весов:",
        nameJson: "min_weight_change_limit",
        options: [],
        defaultValue: 0.005,
        checkInput: isPositiveNumber,
        warning: "Пожалуйста, проверьте свой ввод. Необходимо число >= 0",
        information:
          "Если на очередном шаге обучения относительное изменение нормы вектора весов становится меньше порога, то обучение останавливается.",
      },
      {
        question: "Максимальное количество эпох:",
        nameJson: "max_number_of_epochs",
        options: [],
        defaultValue: null,
        checkInput: isNaturalNumber,
        warning: "Пожалуйста, проверьте свой ввод. Необходимо целое число >= 1",
        information:
          "Максимальное количество итераций обучения алгоритма. Если процесс обучения необходимо ограничить по времени, в этом случае он остановится после заданного количества эпох, даже если обучение еще не пришло к оптимальной точке, т.е. не достигнут порог минимального изменения весов.",
      },
    ],
  },
];

function isNaturalNumber(input) {
  return !isNaN(input) && Number.isInteger(Number(input)) && Number(input) >= 1;
}

function isPositiveNumber(input) {
  return !isNaN(input) && Number(input) >= 0;
}
</script>

<style scoped>
.editor-main {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  width: -moz-fit-content;
  width: fit-content;
  margin: 5px auto;
  padding: 30px;
  background: #fef9c7;
  box-shadow: 5px 10px 10px #000000a6;
}

.editor-main__button-container {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.editor-main__warning {
  font-weight: 600;
  color: #da0000;
}

@media ((max-width: 870px) and (min-width:625px)) {
  .editor-main {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 625px) {
  .editor-main {
    grid-template-columns: 1fr;
  }
}
</style>
