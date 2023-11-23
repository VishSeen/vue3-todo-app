<script>
import './app.scss';
import SearchBar from './components/search-bar/SearchBar.vue'
import ButtonFab from './components/button-fab/ButtonFab.vue'
import PageTitle from './components/page-title/PageTitle.vue'
import ButtonIcon from './components/button-icon/ButtonIcon.vue';
import ModalAdd from './components/modal-add/ModalAdd.vue';
import TodoList from './components/todo-list/TodoList.vue';
import TodoHeader from './components/todo-header/TodoHeader.vue';

export default {
    components:  { SearchBar, ButtonIcon, ButtonFab, ModalAdd, PageTitle, TodoList, TodoHeader },
    data() {
        return {
            title: "tasks",
            modalIsOpened: false,
            searchHistory: "",
            todos: [
                {
                    id: 1,
                    label: "Design some UI for Habits app",
                    isChecked: true
                },
                {
                    id: 1,
                    label: "Sketch something in 5mins",
                    isChecked: false
                },
                {
                    id: 1,
                    label: "Clean the turtle pond ASAP !!",
                    isChecked: true
                },
                {
                    id: 1,
                    label: "Hello world.",
                    isChecked: true
                },{
                    id: 1,
                    label: "Get some cola at the shop",
                    isChecked: false,
                    description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Eget mauris, scelerisque aliquet tortor. Egestas pretium quam pellentesque sagittis ullamcorper augue felis. Eu enim enim, fermentum ac feugiat ornare diam. Sit amet condimentum eget arcu egestas."
                }
            ],
            currentTodos: "All"
        }
    },
    methods: {
        addTasks(todo) {
            this.todos.push(todo);
        },
        openModal(todo) {
            this.modalIsOpened = !this.modalIsOpened;
        },
        searchTodo(text) {

        }
    }
}
</script>


<template>
    <div class="top-bar">
        <div class="left-side">
            <PageTitle :title="title"/>
        </div>

        <div class="right-side">
            <SearchBar @change="console.log(e.target.value)"/>
            <div class="btn-filter">
                <ButtonIcon
                icon="filter_list"
                @click="openModal"
                :outlined="true"
            />
            </div>
        </div>
    </div>

    <div class="todo">
        <TodoHeader :title="currentTodos" :count="todos.length"/>
        <TodoList :todos="todos"/>
    </div>


    <ButtonFab icon="add" @click="openModal" :isClicked="modalIsOpened"/>

    <ModalAdd :isOpened="this.modalIsOpened" :btnClick="addTasks"/>
</template>

