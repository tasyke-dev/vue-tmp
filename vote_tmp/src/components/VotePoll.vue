<template>
    <div class="vote-poll" v-if="poll">
      <h2>{{ poll.question }}</h2>
      <div v-for="(option, index) in poll.options" :key="index">
        <input type="radio" :id="'option-' + index" :value="option" v-model="selectedOption" />
        <label :for="'option-' + index">{{ option }}</label>
      </div>
      <button @click="vote" :disabled="!selectedOption">Vote</button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['poll'],
    data() {
      return {
        selectedOption: null
      };
    },
    methods: {
      vote() {
        this.$emit('voted', this.selectedOption);
        this.selectedOption = null;
      }
    }
  };
  </script>