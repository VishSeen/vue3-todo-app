<script>
import '../src/assets/scss/app.scss'
import SearchBar from './components/search-bar/SearchBar.vue'
import ButtonFab from './components/button-fab/ButtonFab.vue'
import PageTitle from './components/page-title/PageTitle.vue'
import ButtonIcon from './components/button-icon/ButtonIcon.vue'
import TodoItem from './components/todo-item/TodoItem.vue'
import TodoHeader from './components/todo-header/TodoHeader.vue'
import Dropdown from './components/dropdown/Dropdown.vue'

import { uuid } from 'vue-uuid'

export default {
  components: { SearchBar, ButtonIcon, ButtonFab, PageTitle, TodoItem, TodoHeader, Dropdown },
  data() {
    return {
      title: 'tasks',
      modalIsOpened: false,
      searchHistory: '',
      uuid: uuid.v1(),
      inputId: '',
      inputTitle: '',
      inputDesc: '',
      editBtnDisabled: true,
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
  methods: {
    addTask(label, desc) {
      this.todos.push({
        id: uuid.v4(),
        label: label,
        description: desc,
        isChecked: false
      })
      this.modalIsOpened = false
    },
    addEditedTask() {
      this.todos.filter((item) => {
        if (item.id === this.inputId) {
          item.label = this.inputTitle
          item.description = this.inputDesc
        }
      })
      this.inputId = '';
      this.inputTitle = ''
      this.inputDesc = ''
      this.modalIsOpened = false
    },
    deleteTask(todoId) {
      let modifiedList = this.todos.filter((item) => {
        if (item.id !== todoId) {
          return item
        }
      })

      this.todos = modifiedList
      console.log(modifiedList)
    },
    editTask(value) {
      let { id, label, description } = value
      this.inputId = id
      this.inputTitle = label
      this.inputDesc = description
      this.modalIsOpened = true
      this.editBtnDisabled = false;
    },
    searchTask(value) {
      console.log(value)
      this.todos.filter((item) => {
        console.log(item)
        return item.label.toLowerCase() == value
      })
    },
    openModal() {
      if(this.modalIsOpened) {
        this.inputId = '';
        this.inputTitle = '';
        this.inputDesc = '';
        this.editBtnDisabled = true;
        this.modalIsOpened = false;
      } else {
        this.modalIsOpened = true;
        if (this.inputTitle !== '') {
            this.editBtnDisabled = false
        } else {
            this.editBtnDisabled = true
        }
      }
    },
    filterComplete() {
      this.currentTodos = 'Completed';
    },
    filterAll() {
      this.currentTodos = 'All'
    },
    filterOngoing() {
      this.currentTodos = 'Ongoing'
    },
    checkedTodo(id) {
        this.todos.filter(item => {
            if(item.id === id) {
                item.isChecked = !item.isChecked;
            }
        });
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
      <SearchBar v-model="searchHistory" @search-change="this.searchTask" />

      <div class="btn-filter">
        <ButtonIcon
          icon="filter_list"
          @click="this.filterDropdownVisible = !this.filterDropdownVisible"
          :outlined="true"
        />
      </div>

      <div class="filter-dropdown" :class="filterDropdownVisible ? 'visible' : ''">
        <Dropdown :items="filterDropdown" />
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
          @checked-task="this.checkedTodo"
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
        <p>Title</p>
        <input
          v-model="inputTitle"
          @change="this.inputTitle = $event.target.value"
          type="text"
          placeholder="Todo title"
        />
      </div>

      <div class="description">
        <p>Description</p>
        <input
          v-model="inputDesc"
          @change="this.inputDesc = $event.target.value"
          type="text"
          placeholder="Todo description"
        />
      </div>
    </div>

    <div class="button-container">
      <button @click="addEditedTask()" :disabled="editBtnDisabled">EDIT</button>
      <button @click="addTask(this.inputTitle, this.inputDesc)">ADD</button>
    </div>
  </div>
</template>
