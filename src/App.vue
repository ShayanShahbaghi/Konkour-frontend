<template>
  <div id="app">
    <Azmoons :lastAzmoon="this.mainAzmoon"/>
    <lessonsTodo :todo="this.lessonTodo"/>
    <weekTodo :todo="this.weekTodo"/>
  </div>
</template>

<script>
import Azmoons from './components/Azmoons.vue'
import lessonsTodo from './components/lessonsTodo.vue'
import weekTodo from './components/weekTodo.vue'
export default {
  name: 'App',
  components: {
    Azmoons,
    lessonsTodo,
    weekTodo
  },
  data(){
    return {
      mainAzmoon: {},
      lessonTodo: [],
      weekTodo: []
    }
  },
  created(){
    var requestOptions = {
      method: 'GET',
      redirect: 'follow'
    };

    fetch("http://localhost:3000/azmoon/last", requestOptions)
      .then(response => response.text())
      .then(result => {
        console.log(result)
        this.mainAzmoon = JSON.parse(result)
      })
      .catch(error => console.log('error', error))

    fetch("http://localhost:3000/todo/lesson/", requestOptions)
      .then(response => response.text())
      .then(result => {
        console.log(result)
        this.lessonTodo = JSON.parse(result)
      })
      .catch(error => console.log('error', error))  

    fetch("http://localhost:3000/todo/week/", requestOptions)
      .then(response => response.text())
      .then(result => {
        console.log(result)
        this.weekTodo = JSON.parse(result)
      })
      .catch(error => console.log('error', error)) 

    }
    
    
}
</script>

<style>
#app {
  font-family: Dana-Regular;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-bottom: 30px;
}
</style>
