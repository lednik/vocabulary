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
            words : []      
    }
  },
  methods:{
    createWord (){
      const nWord = {
        value: this.newWord,
        trans: this.newTrans
      }
      console.log(nWord)
      this.$http.post('http://localhost:3000/words',nWord)
      .then(response =>{
        return response.json()
      })
      .then(getWord =>{
        console.log(getWord)
      })
    },
    getVacabulary (){
      this.$http.get('http://localhost:3000/words')
      .then(response =>{
        return response.json()
      })
      .then(getAllWords =>{
        this.words = getAllWords
        console.log(getAllWords)
      })
    },
    addToOwnVac (word) {
      const addedWord = {
        value : word.value,
        trans : word.trans
      }
      this.$http.post('http://localhost:3000/userVacabulary',addedWord)
      .then(response =>{
        return response.json()
      })
      .then(getOwnWord =>{
        console.log(getOwnWord)
      })
    },
    getOwnList (){
      this.$http.get('http://localhost:3000/userVacabulary')
      .then(response =>{
        return response.json()
      })
      .then(getAllList =>{
        this.ownWords = getAllList
        console.log(this.ownWords)
      })
    }
  }
}
</script>

<style>

</style>
