<template>
  <div class="newWordForm">
    <div>
      <label for="trans">добавить слово в БД</label>
      <input type="text" v-model="newWord" />
    </div>
    <div>
      <label for="word">добавить его перевод в БД</label>
      <input type="text" v-model="newTrans" />
    </div>
    <button @click="createWord">Создать слово</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newWord: "",
      newTrans: "",
      resourseWords: null,
      resourseOwnWords: null
    };
  },
  methods: {
    createWord() {
      const nWord = {
        value: this.newWord,
        trans: this.newTrans
      };
      this.resourseWords.save({}, nWord);
    }
  },
  created() {
    this.resourseWords = this.$resource("words");
  }
};
</script>
