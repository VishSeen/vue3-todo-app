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
  data() {
    return {
        isCompleted: this.isChecked
    }
  },
  methods: {
    delete() {
        this.$emit('delete-task', this.id);
    },
    edit() {
        this.$emit('edit-task', { id: this.id, label: this.label, description: this.description});
    },
  }
}
</script>

<template>
  <div class="todo-item__wrapper" :class="isCompleted ? 'completed' : ''">
    <div class="title">
      <div class="btn-check">
        <input type="checkbox" @change="checked=this.isCompleted" :checked="isCompleted"/>
      </div>

      <p>
        {{ label }}
      </p>

      <ButtonIcon icon="edit" @click="$emit('edit-task', id)"/>
      <ButtonIcon icon="delete" @click="this.delete"/>
    </div>

    <div v-if="description" class="description">
      <p>
        {{ description }}
      </p>
    </div>
  </div>
</template>
