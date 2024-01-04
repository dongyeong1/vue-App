<template>
  <div>
    <div class="titleWrapper">
        <div>{{childrenValue}}</div>
        <input v-model="childrenValue" @input="childrenUpdate"  />
            <div>{{ dong.title }}</div>
          </div>
          <div class="singoWrppaer">
            <button @click="buttonClick(index)">
              {{ dong.title }}&nbsp;신고하기</button
            ><span>&nbsp;</span>
            <span>신고수: {{ number[index] }}</span>
          </div>
          <div class="buttonWrapper">
            <button @click="modalVisible(index)">상세보기</button>
            <button class="delete" @click="deleteDong(index)">삭제하기</button>
          </div>
  </div>
</template>

<script>
export default {
name:'CardComponent',
props:{
    dong:{
        type:Object,
        default:()=>{
            
        }
    },
    number:{
        type:Array,
        default:()=>[]
    },
    index:{
        type:Number,
        
    },
    modalVisible:{
        type:Function,
    },
    deleteDong:Function

    

},
data(){
    return{
        childrenValue:''
    }
},
methods:{
    childrenUpdate(e){
        this.$emit('fromChildUpdate',e.target.value)
    }
}
}
</script>

<style>

</style>