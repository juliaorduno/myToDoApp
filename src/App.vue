<template>
  <b-row align-h="center">
    <b-col md="7">
      <div class="todo-container">
        <div class="header-container">
          <h4>My ToDo App</h4>
        </div>
        <form @submit.prevent="addTask">
          <b-form-input v-model="newTaskName" id="new-task-input"
                  type="text"
                  placeholder="Escribir tarea nueva">
          </b-form-input>
          <b-button type="submit" variant="success">Agregar Tarea</b-button>
        </form>
        <tasks-list 
          :title="'Pendientes'" 
          :task-list="tasksPending" 
          @complete="toggleTask" />
        <tasks-list 
          :title="'Completados'" 
          :task-list="tasksCompleted" 
          @complete="toggleTask" />
      </div>
    </b-col>
    
  </b-row>
</template>

<script>
import TasksList from './components/TasksList'
  export default {
    components: {
      TasksList
    },
    data() {
      return {
        tasks: [
          {
            name: 'Tarea 1',
            done: false
          },
          {
            name: 'Tarea 2',
            done: false
          },
          {
            name: 'Tarea 3',
            done: false
          }
        ],
        newTaskName: ''
      }
    },
    beforeMount() {
      let tasks = JSON.parse(localStorage.getItem('toDoTasks'))
      if(tasks) this.tasks = tasks
    },
    computed: {
      tasksPending() {
        return this.tasks.filter( task => !task.done)
      },
      tasksCompleted() {
        return this.tasks.filter( task => task.done)
      }
    },
    methods: {
        toggleTask(task) {
          task.done = !task.done
          this.saveInLocalStorage()
        },
        addTask() {
          if(!this.newTaskName) return
          this.tasks.push({
            name: this.newTaskName,
            done: false
          })
          this.newTaskName = ''
          this.saveInLocalStorage()
        },
        saveInLocalStorage() {
          localStorage.setItem('toDoTasks', JSON.stringify(this.tasks));
        }
      }
  }
</script>

<style>

body {
  background-color: #FCFCFC !important;
}

h4, h5 {
  text-transform: uppercase;
}

.header-container {
  padding: 0.75rem 0;
}

.todo-container {
  background-color: #FFFF;
  margin: 1rem 0rem;
  max-height: 90vh;
  height: 90vh;
  border-radius: 5px;
  padding: 2rem;
  overflow-y: auto;
}

#new-task-input {
  display: inline-block;
  width: 80%;
}

.btn {
  float: right;
}

</style>

