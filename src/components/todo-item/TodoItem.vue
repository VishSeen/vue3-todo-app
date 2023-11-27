<script>
import './style.scss'
import ButtonIcon from '../button-icon/ButtonIcon.vue'

export default {
  components: { ButtonIcon },
  props: {
    id: String,
    label: String,
    description: String,
    isChecked: Boolean
  },
  methods: {
    delete() {
        this.$emit('delete-task', this.id);
    },
    edit() {
        this.$emit('edit-task', { id: this.id, label: this.label, description: this.description });
    },
    checkedTodo() {
        this.$emit('checked-task', this.id);
    }
  }
}
</script>

<template>
  <div class="todo-item__wrapper" :class="isChecked ? 'completed' : ''">
    <div class="title">
      <div class="btn-check">
        <input type="checkbox" @change="this.checkedTodo" :checked="isChecked"/>
      </div>

      <p>
        {{ label }}
      </p>

      <ButtonIcon icon="edit" @click="this.edit"/>
      <ButtonIcon icon="delete" @click="this.delete"/>
    </div>

    <div v-if="description" class="description">
      <p>
        {{ description }}
      </p>
    </div>
  </div>
</template>
