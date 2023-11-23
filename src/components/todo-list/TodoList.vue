<script>
import './style.scss'
import TodoItem from '../todo-item/TodoItem.vue'

export default {
  components: { TodoItem },
  props: {
    type: String,
    todos: Array
  }
}
</script>

<template>
    <div class="todo-list">
        <TodoItem
      v-for="item in todos"
      :key="item.id"
      :label="item.label"
      :isChecked="item.isChecked"
      :description="item.description"
    />
    </div>
</template>
