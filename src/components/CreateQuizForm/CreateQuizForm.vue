<template>
  <div class="create-quiz-wrapper">
    <h1 class="create-quiz-heading">Create Quiz</h1>
    <form class="create-quiz-form" @submit.prevent="submitQuiz">
      <label>
        Title
        <input
          type="text"
          name="quizTitle"
          v-model.trim="quizTitle"
          @blur="validateInput"
          @focus="clearInputError"
        />
        <span class="error" v-if="validationErrors.quizTitle">
          {{ validationErrors.quizTitle }}
        </span>
      </label>
      <label>
        Category
        <input type="text" v-model="category" />
        <button @click="addCategory" type="button">Add category</button>
        <ul class="categories-list">
          <li v-for="ctg in quizCategories" :key="ctg">{{ ctg }}</li>
        </ul>
      </label>
      <label>
        Quiz type
        <select
          name="quizType"
          v-model="quizType"
          @blur="validateInput"
          @focus="clearInputError"
        >
          <option value>Choose an option</option>
          <option v-for="type in quizTypes" :value="type" :key="type">
            {{ capitalizeQuizType(type) }}
          </option>
        </select>
        <span class="error" v-if="validationErrors.quizType">
          {{ validationErrors.quizType }}
        </span>
      </label>
      <label>
        Number of questions
        <p>(you can change it later)</p>
        <input
          type="number"
          v-model.number="questionsNumber"
          min="0"
          name="questionsNumber"
          @blur="validateInput"
          @focus="clearInputError"
        />
        <span class="error" v-if="validationErrors.questionsNumber">
          {{ validationErrors.questionsNumber }}
        </span>
      </label>
      <button class="create-quiz-button" type="submit">Create Quiz</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CreateQuizForm",
  data() {
    return {
      category: "",
      questionsNumber: 0,
      quizTitle: "",
      quizCategories: [] as string[],
      quizTypes: ["multiple-choice", "true-false", "short-answer", "mixed"],
      quizType: "",
      validationErrors: { quizTitle: "", quizType: "", questionsNumber: "" }
    };
  },
  methods: {
    validateInput(e: { target: HTMLInputElement }) {
      if (!e.target.value || e.target.value === "0") {
        this.validationErrors = {
          ...this.validationErrors,
          [e.target.name]: "Field is required"
        };
      }
    },

    clearInputError(e: { target: HTMLInputElement }) {
      this.validationErrors = {
        ...this.validationErrors,
        [e.target.name]: ""
      };
    },

    addCategory() {
      const isCategoryAlreadyExists = this.quizCategories.find(
        cat => cat === this.category
      );
      if (this.category && !isCategoryAlreadyExists) {
        this.quizCategories = [...this.quizCategories, this.category];
        this.category = "";
      }
    },

    capitalizeQuizType(type: string) {
      return type
        .split("-")
        .map(word => word[0].toUpperCase() + word.slice(1))
        .join(" ");
    },

    submitQuiz() {
      console.log("submitted");
    }
  }
});
</script>
<style lang="scss">
@import "./createQuizForm.module.scss";
</style>
