<!-- the options
<script>
export default {

  data() {
    return {
      name: "lydia",
      status: true,
      tasks: ['Task1', 'Task2', 'Task3'],
      link: "https://www.google.com"
    };
  },

  methods: {
    toggleStatus() {
      this.status = !this.status;
    }
  }

};
</script>-->


<!--the caption-->
<script setup>
import {ref, onMounted} from 'vue';  //ref: pour rendre les element dynamique
      const name= ref('lydia');
      const status= ref(true);
      const tasks= ref(['Task1', 'Task2', 'Task3']);
      const link= ref("https://www.google.com");
   
      const toggleStatus = () => {
        status.value = !status.value;
      };

      const newTask = ref('');
      const addTask = () => {
        if (newTask.value.trim() !== '') {
          tasks.value.push(newTask.value);
          newTask.value = '';
        }
      };
      const deleteTask = (index) => {
          tasks.value.splice(index,1);
      };

      onMounted(async () => {
        try{
          const response = await fetch('https://jsonplaceholder.typicode.com/todos');
          const data = await response.json();
          tasks.value = data.map(item => item.title);
        }catch(error){
          console.error('Error fetching tasks:', error);
        }
      });

</script>

<template>
<h1>hello {{ name }}</h1>

<!--Conditional Rendering--> 

<p v-if="status">You are logged in</p>
<p v-else>You are not logged in</p>

<!--List Rendering (boucle)--> 
<h3>Tasks:</h3>
<ul>
  <!--<li v-for="(task, index) in tasks" :key="index">{{ task }}</li>-->
  <li v-for="(task,index) in tasks" :key="task">
    <span>{{ task }}</span>
    <button @click="deleteTask(index)">x</button>
  </li>
</ul>

<!--direction-->
<a v-bind:href="link">click for google</a>
<a :href="link">click for google</a>

<button v-on:click="toggleStatus">change status</button>
<button @click="toggleStatus">change status</button>

<br/>

<!--form-->
<form @submit.prevent ="addTask">
  <label for="newTask">add Task</label>
  <input type="text" id="newTask" name="newTask" v-model="newTask"/>
  <button type="submit">submit</button>
</form>

</template>

