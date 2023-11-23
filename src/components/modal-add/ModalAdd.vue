<script>
import './style.scss';

export default {
    name: "ModalAdd",
    data() {
        return {
            todoTitle: '',
            todoDesc: ''
        }
    },
    props: {
        isOpened: Boolean,
        btnClick: Function
    },
    methods: {
        inputTitleChanged(e) {
            this.todoTitle = e.target.value;
        },
        inputDescChanged(e) {
            this.todoDesc = e.target.value;
        },
        btnAddClick() {
            this.$emit('addTasks', this.todoTitle)
        }
    }
}
</script>


<template>
    <div class="modal-add" :class="isOpened ? 'opened' : ''">
        <div class="input-container">
            <div class="title">
                <p>
                    Title
                </p>
                <input @change="inputTitleChanged($event)" type="text" placeholder="Todo title">
            </div>

            <div class="description">
                <p>
                    Description
                </p>
                <input @change="inputDescChanged($event)" type="text" placeholder="Todo description">
            </div>
        </div>

        <button @click="btnAddClick">ADD</button>
    </div>
</template>