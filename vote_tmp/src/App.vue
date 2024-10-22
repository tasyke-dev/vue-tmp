<template>
  <div id="app">
    <div class="container">
      <VotePollForm @poll-created="handlePollCreated" />
      <div class="right-container">
        <div class="poll-wrapper" v-for="(pollData, index) in polls" :key="index">
          <VotePoll :poll="pollData.poll" @voted="(selectedOption) => handleVote(selectedOption, index)" />
          <VotePollResult :pollResults="pollData.results" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VotePollForm from './components/VotePollForm.vue';
import VotePoll from './components/VotePoll.vue';
import VotePollResult from './components/VotePollResult.vue';

export default {
  data() {
    return {
      polls: [] 
    };
  },
  components: {
    VotePollForm,
    VotePoll,
    VotePollResult
  },
  methods: {
    handlePollCreated(newPoll) {
      const initialResults = newPoll.options.reduce((acc, option) => {
        acc[option] = 0;
        return acc;
      }, {});
      this.polls.push({ poll: newPoll, results: initialResults });
    },
    handleVote(selectedOption, index) {
      this.polls[index].results[selectedOption]++;
    }
  }
};
</script>
