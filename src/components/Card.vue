<template>
  <li class="Card">
    <span>
      <input class="checkbox" type="checkbox" :value="done" @click="toggleTodo" :checked="done">
    </span>
    <span :class="{'done':done}" class="title">{{todo.title}}</span>
    <span v-if="done" @click="deleteTodo()" class="marterial-iconsdesc"> close </span>
  </li>
</template>

<script>
 import { computed } from "vue"
export default {
  name:"ToCard",
  props:{
    todo:{
      type:Object,
      required: true,
    }
  },
  setup(props, context){
    const done = computed(()=>props.todo.done)
    return{
      done,
      toggleTodo:() =>{
        const value={
          ...props.todo,
          done: !props.todo.done
        }
        context.emit('change',value);
      },
      deleteTodo: ()=>{
        context.emit('delete',props.todo.id);
      },
    }
  } 
}
</script>

<style scoped>

</style>