<template>
  <div class="poll-form">
    <h2>Create a new poll</h2>
    <form @submit.prevent="createPoll">
      <label>Question:</label>
      <input type="text" v-model="poll.question" required />

      <label>Options:</label>
      <div v-for="(option, index) in poll.options" :key="index">
        <input type="text" v-model="poll.options[index]" placeholder="Option" required />
        <button type="button" @click="removeOption(index)">Remove</button>
      </div>

      <button type="button" @click="addOption">Add Option</button>
      <button type="submit" :disabled="!canCreatePoll">Create Poll</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      poll: {
        question: '',
        options: ['']
      }
    };
  },
  computed: {

    canCreatePoll() {
      const nonEmptyOptions = this.poll.options
        .map(option => option.trim())
        .filter(option => option !== '');

      const uniqueOptions = [...new Set(nonEmptyOptions)];
      return uniqueOptions.length >= 2 && uniqueOptions.length === nonEmptyOptions.length;
    }
  },
  methods: {
    addOption() {
      this.poll.options.push('');
    },
    removeOption(index) {
      this.poll.options.splice(index, 1);
    },
    createPoll() {
      if (this.canCreatePoll) {
        this.$emit('poll-created', { ...this.poll });
        this.poll.question = '';
        this.poll.options = [''];
      } else {
        alert('Please ensure there are at least 2 unique options.');
      }
    }
  }
};
</script>