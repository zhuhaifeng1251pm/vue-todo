<template>
    <div class="home">
        <header><input type="text" v-model="todo" > <button class="submit" @click="handleInput">确认</button></header>
        <EventLists :todolists='todolists' :handleDelete='handleDelete' :handleDelAll='handleDelAll' :changeType='changeType' :type='type'/>
        <!-- <footer> <span class="num">{{leaveEvent}} items left</span>  <div class="toShow">
            <span  @click="handleChange('all')">All</span>
            <span @click="handleChange('active')">Active</span>
            <span @click="handleChange('completed')" >Completed</span>
        </div><button class="clear" 
        @click="handleDelAll" :style="`display:${completedEvent?'block':'none'}`">ClearCompleted</button>
        </footer> -->
    </div>
</template>
<script>
import EventLists from "./EventLists";
import shortid from "shortid";
import '../assets/global.css'
export default {
  name: "home",
  components: {
    EventLists
  },
  data: () => ({
    todolists: [],
    todo: "",
    type:'all'
  }),
  methods: {
    handleInput() {
        if(this.todo.trim()){
      this.todolists.push({ id: shortid(), todoText: this.todo, isComplete: false });}
      else{alert("输入的字符不符合要求，请重新输入")}
      this.todo=''
    },
    handleDelete(id){
        this.todolists.splice(this.todolists.findIndex(t=>t.id===id),1)
    },
    handleDelAll(){
       this.todolists= this.todolists.filter(t=>t.isComplete===false)
    },changeType(type){
        this.type = type
        console.log(type)

    }
  }
};
</script>
<style scoped>
.home {
  width: 550px;
  margin: 0 auto;
  margin-top: 20%;
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 10px;
}

header input {
  width: 450px;
  height: 65px;
  outline: 0;
  border: 0;
  border-bottom: 2px solid #999;
  padding: 15px 25px;
  font-size: 21px;
  border-radius: 0 0 5px 5px;
}
header .submit{
    height: 65px;
    width: 70px;
    border: 0;
    outline: 0;
    background-color:#1992ff;
    margin-left: 5px;
    border-radius: 5px;
        color:#fff;

}
/* footer{
    width: 100%;
    height: 30px;
    display: flex;
    align-items: center;
    padding: 10px 10px  0 10px ;
}
span{
    margin-right:30px;
}
.num{
    margin-right: 50px;
}
.clear{
    margin-left: 20px;
    outline:0;
    border: 0;
    width: 120px;
    line-height: 30px;
    border-radius: 5px;
    background-color: #1992ff;
    color:#fff;
} */
</style>



