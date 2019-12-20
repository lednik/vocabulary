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
      added : [],
      userTranslets : [],
      userTrans : [],
      isVis: false,
      transl : ''   
    }
  },
  methods:{
    addWord (word){
      this.added.push(word)
    },
    check(index){
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
