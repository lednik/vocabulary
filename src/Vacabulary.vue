<template>
  <div class="vacabulary">
    <button @click="getVacabulary">Загрузить словарь</button>
    <ul>
      <li v-for="word in words" :key="word.id">
        <strong>{{ word.value }}</strong>
        : {{ word.trans }}
        <button @click="addToOwnVac(word)">+++</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      words: [],
      resourseWords: null,
      resourseOwnWords: null
    };
  },
  methods: {
    getVacabulary() {
      this.resourseWords
        .get()
        .then(response => response.json())
        .then(words => (this.words = words));
    },
    addToOwnVac(word) {
      const addedWord = {
        value: word.value,
        trans: word.trans
      };
      this.resourseOwnWords.save({}, addedWord);
    }
  },
  created() {
    this.resourseWords = this.$resource("words");
    this.resourseOwnWords = this.$resource("userVacabulary");
  }
};
</script>