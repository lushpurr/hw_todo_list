<template>
  <div id="app">
      <form v-on:submit.prevent="add">
        <label for="new-todo">Add a todo:</label>
        <input id="new-todo" type="text" v-model="newTodo" />
       
      <input name="priority" type="radio" id="true" value="true" v-model="radioButton">
      <label for="high-priority">High</label>
        
        <input name="priority" type="radio" id="false" value="false" v-model="radioButton">
        <label for="low-priority">Low</label> 

         
      <input type="submit" value="Add" />
      </form>

      <ul>
        <!-- creating new li for todoList Item -->

        <li v-for="(item, index) in todoList" :key="index" :class="item.highPriority ? 'high' : 'low' "> 
          <span>{{ item.name }}</span>  
          <span v-if="item.isDone">Done</span>
          <span v-if="item.highPriority == true">High Priority</span>
          <span v-else>Low Priority</span>
          <button v-if="!item.isDone" v-on:click="doTask(index)">Completed Task</button>
        </li>
      </ul>
  </div>
</template>

<script>

export default {
  data() {
    return {
      todoList: [
        {name:"washing", isDone: false, highPriority: false},
        {name:"hoovering", isDone: true, highPriority: true},
        {name:"laundry", isDone: false, highPriority: true},
        {name:"dishes", isDone: false, highPriority: true},
      ],
      newTodo: ""
    }
  },
  methods: {
  
    add: function(){

      this.todoList.push({
        name: this.newTodo,
        isDone: false,
        highPriority: this.radioButton
    }),
      this.newTodo = "";
      this.radioButton = true;
    },

    doTask: function(index){
      this.todoList.[index].isDone = true;

    },

    // radioButton: function(){

    // }
}};
</script>






<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0d141c;
  margin-top: 60px;
}

li{
  display:flex;
  justify-content: space-evenly;
}

li.high {
  background-color: rgb(250, 101, 101);

}

li.low {
  background-color: rgb(244, 203, 128);
}
</style>
