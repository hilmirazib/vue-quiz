<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${(questionAnswered / questions.length) * 100}%` }"></div>
      <div class="status">{{ questionAnswered }} out of {{ questions.length }} questions answered</div>
    </div>
    <transition-group name="fade">
      <div class="single-question" v-for="(question, q) in questions" :key="question.q" v-show="questionAnswered === q">
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div class="answer" v-for="answer in question.answers" :key="answer.text" @click.prevent="selectAnswer(answer.is_correct)">
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>
<script>
export default {
  name: 'Questions',
  props: ['questions', 'questionAnswered'],
  emits: ['selectAnswer'],
  methods: {
    selectAnswer(isCorrect) {
      this.$emit('question-answered', isCorrect);
    },
  },
};
</script>
<style></style>
