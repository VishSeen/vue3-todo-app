<script>
import './app.scss'
import SearchBar from './components/search-bar/SearchBar.vue'
import ButtonFab from './components/button-fab/ButtonFab.vue'
import PageTitle from './components/page-title/PageTitle.vue'
import ButtonIcon from './components/button-icon/ButtonIcon.vue'
import TodoItem from './components/todo-item/TodoItem.vue'
import TodoHeader from './components/todo-header/TodoHeader.vue'
import Dropdown from './components/dropdown/Dropdown.vue'

import { uuid } from 'vue-uuid';



export default {
  components: { SearchBar, ButtonIcon, ButtonFab, PageTitle, TodoItem, TodoHeader, Dropdown },
  data() {
    return {
      title: 'tasks',
      modalIsOpened: false,
      searchHistory: '',
      uuid: uuid.v1(),
      inputTitle: '',
      inputDesc: '',
      todos: [
        {
          id: '1',
          label: 'Design some UI for Habits app',
          isChecked: true
        },
        {
          id: '2',
          label: 'Sketch something in 5mins',
          isChecked: false
        },
        {
          id: '3',
          label: 'Clean the turtle pond ASAP !!',
          isChecked: true
        },
        {
          id: '4',
          label: 'Hello world.',
          isChecked: true
        },
        {
          id: '5',
          label: 'Get some cola at the shop',
          isChecked: false,
          description:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Eget mauris, scelerisque aliquet tortor. Egestas pretium quam pellentesque sagittis ullamcorper augue felis. Eu enim enim, fermentum ac feugiat ornare diam. Sit amet condimentum eget arcu egestas.'
        }
      ],
      currentTodos: 'All',
      filterDropdownVisible: false,
      filterDropdown: [
        {
            label: 'All',
            clickEvent: this.filterAll
        },
        {
            label: 'Ongoing',
            clickEvent: this.filterOngoing
        },
        {
            label: 'Completed',
            clickEvent: this.filterComplete
        }
      ]
    }
  },
  computed: {
  },
  methods: {
    addTask(label, desc) {
      this.todos.push({
        id: uuid.v4(),
        label: label,
        description: desc,
        isCompleted: true
      });

      this.inputTitle = '';
      this.inputDesc = '';
      this.modalIsOpened = false;
    },
    deleteTask(todoId) {
        let modifiedList = this.todos.filter(item => {
            if(item.id !== todoId) {
                return item;
            }
        });

        this.todos = modifiedList;
        console.log(modifiedList)
    },
    editTask(value) {
        let { id, label, description } = value;
        console.log('EDIT', label)
    },
    searchTask(value) {
        this.todos.filter(item => {
            return item.label == value
        })
    },
    openModal() {
      this.modalIsOpened = !this.modalIsOpened
    },
    filterComplete() {
        this.currentTodos = 'Completed';
    },
    filterAll() {
        this.currentTodos = 'All';
    },
    filterOngoing() {
        this.currentTodos = 'Ongoing';
    },
    checkedTodo(id) {

    }
  }
}
</script>

<template>
  <div class="top-bar">
    <div class="left-side">
      <PageTitle :title="title" />
    </div>

    <div class="right-side">
      <SearchBar v-model="searchHistory" @change="this.searchTask($event.target.value)" />

      <div class="btn-filter">
        <ButtonIcon icon="filter_list" @click="this.filterDropdownVisible = !this.filterDropdownVisible" :outlined="true" />
      </div>

      <div class="filter-dropdown" :class="filterDropdownVisible ? 'visible' : ''">
        <Dropdown :items="filterDropdown"/>
      </div>
    </div>
  </div>


  <div class="todo">
    <TodoHeader :title="currentTodos" :count="todos.length" :type="currentTodos.toLowerCase()" />

    <div class="todo-list__wrapper">
        <div v-if="todos.length" class="todo-list">
            <TodoItem
                v-for="item in this.todos"
                :id="item.id"
                :key="item.id"
                :label="item.label"
                :isChecked="item.isChecked"
                :description="item.description"
                @delete-task="this.deleteTask"
                @edit-task="this.editTask"
                @checked-todo="this.checkedTodo"
            />
        </div>

        <div class="todo-error" v-else>
            <p>Sorry no todos found..</p>
        </div>
    </div>
  </div>


  <ButtonFab icon="add" @click="openModal" :isClicked="modalIsOpened" />


  <div class="modal" :class="this.modalIsOpened ? 'opened' : ''">
    <div class="input-container">
            <div class="title">
                <p>
                    Title
                </p>
                <input v-model="inputTitle" @change="this.inputTitle = $event.target.value" type="text" placeholder="Todo title">
            </div>

            <div class="description">
                <p>
                    Description
                </p>
                <input v-model="inputDesc" @change="this.inputDesc = $event.target.value" type="text" placeholder="Todo description">
            </div>
        </div>

        <button @click="addTask(this.inputTitle, this.inputDesc)">ADD</button>
  </div>
</template>
