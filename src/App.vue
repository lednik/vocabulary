<template>
  <div>
    <p>{{isVis}}</p>
    <p>{{added}}</p>
    <ul>
      <li v-for="word of words">{{word.value}} : {{word.trans}} <button @click="addWord(word)">добавить</button></li>
    </ul>
    
    <p>Проверить слова : <button @click="isVis=!isVis">поехали</button></p>
    <ul v-show="isVis">
      <li v-for="(word , index) of added">{{index}}{{word.value}}: <input  v-model="userTranslets[index]" @input="check(index)"  type="text">{{userTrans[index]}} </li>
    </ul>
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
</template>

<script>

export default {
  data () {
    return {
      msg: 'Привет',
      words: [
        {value:'red', trans:'красный'},
        {value:'blue', trans:'синий'},
        {value:'green', trans:'зеленый'}
      ],
      newWord : '',
      newTrans : '',
      added : [],
      isAdded : false,
      userTranslets : [],
      userTrans : [],
      isVis: false,
      transl : ''   
    }
  },
  methods:{
    createWord (){
      const nWord = {
        value: this.newWord,
        trans: this.newTrans
      }
      this.$http.post('http://localhost:3000/words',nWord)
      .then(response =>{
        console.log(response)
      })
    },
    addWord (word) {
      let first=this.isAdded
      for(let i=0;i<this.added.length;i++){
        if(word==this.added[i]){
          this.isAdded=!first
          }
      }
      if(this.isAdded==first){this.added.push(word)}
    },
    check (index) {
      if(this.userTranslets[index]==this.added[index].trans){
        this.userTrans[index]=true
      }
      else{
        this.userTrans[index]=false
      }
    }
  }
}
</script>

<style>

</style>
