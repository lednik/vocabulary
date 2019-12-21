<template>
  <div>
    <div class="newWordForm">
          <div>
            <label for="trans">добавить слово в БД</label>
            <input type="text" v-model="newWord">
          </div>
          <div>
            <label for="word">добавить его перевод в БД</label>
            <input type="text" v-model="newTrans">
          </div>
              <button @click="createWord">Создать слово</button>
    </div>
    <div class="vacabulary">
      <button @click="getVacabulary">Загрузить словарь</button>
      <ul>
        <li 
        v-for="word in words"
        :key="word.id"
        > <strong>{{word.value}}</strong> : {{word.trans}}
        <button @click="addToOwnVac(word)">+++</button>
        </li>
      </ul>

    </div>
    <div class="own">
      <button @click="getOwnList">Загрузить cвой справочник</button>
      <ul>
        <li 
        v-for="word in ownWords"
        :key="word.id"
        > <strong>{{word.value}}</strong> : {{word.trans}}
        </li>
      </ul>
    </div>

  </div>
</template>

<script>

export default {
  data () {
    return {
            newWord : '',
            newTrans : '',
            ownWords : [],
            words : [],
            resourseWords : null,
            resourseOwnWords : null
    }
  },
  methods:{
    createWord (){
      const nWord = {
        value: this.newWord,
        trans: this.newTrans
      }
      this.resourseWords.save({},nWord)
    },
    getVacabulary (){
      this.resourseWords.get().then(response => response.json()).then(words => this.words = words)
    },
    addToOwnVac (word) {
      const addedWord = {
        value : word.value,
        trans : word.trans
      }
      this.resourseOwnWords.save({},addedWord)
    },
    getOwnList (){
      this.resourseOwnWords.get().then(response => response.json()).then(words => this.ownWords = words)
    }
  },
  created(){
    this.resourseWords = this.$resource('http://localhost:3000/words')
    this.resourseOwnWords = this.$resource('http://localhost:3000/userVacabulary')
  }
}
</script>

<style>

</style>
