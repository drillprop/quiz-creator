<template>
  <create-quiz-vue />
</template>

<script lang="ts">
import CreateQuizVue from "@/components/CreateQuizForm/CreateQuizForm.vue";
import { defineComponent } from "vue";
export default defineComponent({
  components: {
    CreateQuizVue
  }
});
</script>
