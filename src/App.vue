<template>
  <div class="h-screen w-width bg-blue-300 flex flex-col justify-center items-center">
    <div class="header">
      <h1 class="text-4xl">Seth's Todo App With Tailwind And Vue</h1>
      <div class="form flex">
        <input 
        v-model="newTodo"
        @keyup="checkAdd"
        class="appearance-none border w-full py-2 px-3 text-gray-700 leading-tight focus:outline-non" id="newText" type="text" placeholder="Add New Todo"/>
        <button id="newBtn"
        @click="add"
         class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4">Add</button>
      </div>
    </div>
    <div class="todos w-1/2 mt-8">
      <div class="pendings" v-if="totalPendings > 0">
        <h3 class="text-2xl">Pendings: - {{totalPendings}}:</h3>
        <ul id="pendingList">
          <li
          v-for="(pending, index) in pendingList"
          :key="index"
          @click="moveToCompleted(pending, index)"
          class="text-center p-3 bg-white mt-4 rounded shadow-lg cursor-pointer hover:bg-blue-500">{{pending}}</li>
        </ul>
        </div>
      <div class="completed mt-8" v-if="totalCompleted > 0">
        <h3 class="text-2xl">Completed - {{totalCompleted}}:</h3>
        <ul id="completedList">
          <li 
          v-for="(completed, index) in completedList"
          :key="index"
          @click="moveToPending(completed, index)"
          class="text-center p-3 bg-white line-through text-red-500 mt-4 rounded shadow-lg cursor-pointer hover:bg-red-500 hover:text-black">{{completed}}</li>
        </ul>
      </div>
    </div>
  </div>  
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      newTodo: "",
      pendingList: [],
      completedList: []
    };
  },
  computed: {
    totalPendings(){
      return this.pendingList.length;
    },
    totalCompleted(){
      return this.completedList.length;    
    }
  },
  methods: {
    add(){
      if(this.newTodo != ""){
        this.pendingList.push(this.newTodo);
        this.newTodo="";
      } else {
        alert('Please specify the task to add');
      }
    },
    checkAdd(event){
      if(event.keyCode === 13){
        event.preventDefault();
        this.add();
      }
    },
    moveToCompleted(todo, index){
        this.completedList.push(todo);
        this.pendingList.splice(index, 1);
    },
    moveToPending(todo, index){
        this.pendingList.push(todo),
        this.completedList.splice(index, 1);
    }
  }
};
</script>