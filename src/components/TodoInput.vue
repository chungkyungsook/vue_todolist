<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" 
           placeholder="Type what you have to do" v-on:keyup.enter='addTodo'>
    <span class="addContainer" v-on:click='addTodo'>
      <i class="addBtn fa fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" @close='showModal = false'>
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal=false">
        할 일을 입력하세요.
        <i class="closeModalBtn fa fa-times" aria-hidden="true"></i>
      </span>
    </modal>

  </div>
</template>

<script>
import Modal from './common/Modal'

export default{
  data(){
    return{
      newTodoItem: '',
      showModal: false
    }
  },
  methods:{
    addTodo(){
      if (this.newTodoItem !== ''){
        var value = this.newTodoItem && this.newTodoItem.trim();
        this.$emit('addTodo',value) //하위 에서 상위
        this.clearInput();
      }else{
        this.showModal = !this.showModal;
      }
    },
    clearInput(){
      this.newTodoItem = '';
    }
  },
  components: {
    Modal: Modal
  }
}

</script>

<style scoped>
  input:focus{
    outline: none;
  }
  .inputBox{
    background-color: #fff;;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input{
    border-style: none;
    font-size: 0.9rem;
  }

  .addContainer{
    float: right;
    background: linear-gradient(45deg, #227ab4, #8763FB);
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addContainer:hover{
    background: linear-gradient(45deg, #8763FB,#53428b);
  }
  .addBtn{
    color:white;
    vertical-align: middle;
  }
  .addBtn:hover{
    cursor: pointer;
  }
</style>
