<template>
  <div>
    <div v-if="visible == true">
      <div class="black-bg">
        <div class="white-bg">
          {{ modalContent }}
          <button @click="modalClose">모달창닫기</button>
        </div>
      </div>
    </div>

    <div class="wrapper">
      <div v-if="dongs === 1">
        <div class="wrap"><div class="form">
          <div class="formWrapper">
            <div>
              <div>{{aaaaDong}}</div>
              <label for="dong">동이름</label>
              <input v-model="newDong" id="dong" class="input" type="text" />
            </div>
            <!-- <button @click="addDong">추가하기</button> -->
            <div class="error" v-if="dongError == true">동을 입력해주세요</div>
          </div>
          <div class="formWrapper">
            <div>
              <label for="content">동내용</label>
              <input
              v-model="newContent"
                id="content"
                class="input"
                type="text"
              />
            </div>
            <div class="error" v-if="contentError == true">
              내용을 입력해주세요
            </div>
          </div>
        </div>
        <div class="button">
                  <button class="addButton" @click="addDong">추가하기</button>

        </div>
</div>

        <CardVue
          class="contentWrapper"
          v-for="(dong, index) in dongName"
          :key="index"
          :dong="dong"
          :number="number"
          :index="index"
          :modalVisible="modalVisible"
          :deleteDong="deleteDong"
          @fromChildUpdate='childUpdate'
          
        >


        </CardVue>
      </div>
    </div>
  </div>


</template>

<script>
import CardVue from './components/Card.vue';



export default {
  name: "App",
   components: {
    CardVue
  },
  data() {
    return {
      visible: false,
      dongs: 1,
      number: [0, 0, 0],
      dongName: [
        { title: "둔산동", content: "둔산123" },
        { title: "갈마동", content: "갈마123" },
        { title: "월평동", content: "월평123" },
      ],
      newDong: "",
      newContent: "",
      dongError: false,
      contentError: false,
      modalContent: "",
    };
  },
  methods: {
childUpdate(data){
  console.log('dddddd',data)
},

    buttonClick(index) {
      this.number[index]++;
    },
    inputValue(e) {
      this.newDong = e.target.value;
      console.log(e.target.value);
    },
    contentValue(e) {
      this.newContent = e.target.value;
    },
    addDong() {
      if (this.newDong.length > 0 && this.newContent.length > 0) {
        this.dongError = false;
        this.contentError = false;

        this.dongName.push({ title: this.newDong, content: this.newContent });
      } else {
        console.log("length", this.newContent.length);
        if (this.newDong.length == 0) {
          this.dongError = true;
        } else {
          this.dongError = false;
        }
        if (this.newContent.length == 0) {
          this.contentError = true;
        } else {
          this.contentError = false;
        }
      }

      this.number.push(0);
    },
    deleteDong(index) {
      console.log(index);
      this.dongName = this.dongName.filter(
        (v) => v.title !== this.dongName[index].title
      );
      this.number = this.number.filter((v, i) => i !== index);
    },
    addContent() {},
    modalVisible(index) {
      this.visible = true;
      this.modalContent = this.dongName[index].content;
    },
    modalClose() {
      this.visible = false;
    },
  },

  computed:{
    
    aaaaDong:function(aaa){
      console.log('computed',aaa)
      return this.newDong+'aaa'
    }
  },
  // watch:{
  //   newDong:function(aaa){
  //     console.log('asdasdazz',aaa)
  //   }
  // },
  created(){
    console.log('시작')
  }

};
</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.buttonWrapper {
  margin-top: 20px;
  display: flex;
  gap: 10px;
  justify-content: center;
}
.delete {
  background: red;
  border: 1px solid red;
  border-radius: 10px;
}
.contentWrapper {
  border-radius: 20px;
  margin-top: 20px;
  border: 1px solid black;
  width: 300px;
  padding: 20px;
}
.wrapper {
  display: flex;
  justify-content: center;
}
.input {
  width: 150px;
}
.formWrapper {
  width: auto;
  
}
.black-bg {
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
}
.white-bg {
  width: 300px;
  height: 300px;
  background: white;
  border-radius: 10px;
  padding: 20px;
}
.singoWrppaer {
  margin-top: 20px;
  width: 258px;
  display: flex;
  justify-content: center;
}
.titleWrapper {
  width: 258px;
  display: flex;
  justify-content: center;
}
button {
  cursor: pointer;
}
.error {
  color: red;
  width: 150px;
}
.form {

}
.wrap{
  display: flex;
  justify-content: center
  
  ;
}
</style>
