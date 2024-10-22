<template>
  <div class="vote-result" v-if="pollResults">
    <h3>Results:</h3>
    <ul>
      <li v-for="(votes, option) in pollResults" :key="option">
        {{ option }}: {{ votes }} votes
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['pollResults']
};
</script>
