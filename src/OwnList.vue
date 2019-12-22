<template>
  <div class="ownList">
    <button @click="getOwnList">Загрузить cвой справочник</button>
    <ul>
      <li v-for="word in ownWords" :key="word.id">
        <strong>{{ word.value }}</strong>
        : {{ word.trans }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ownWords: [],
      resourseOwnWords: null
    };
  },
  methods: {
    getOwnList() {
      this.resourseOwnWords
        .get()
        .then(response => response.json())
        .then(words => (this.ownWords = words));
    }
  },
  created() {
    this.resourseOwnWords = this.$resource("userVacabulary");
  }
};
</script>
