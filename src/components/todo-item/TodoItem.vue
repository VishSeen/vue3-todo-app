<script>
import './style.scss'
import ButtonIcon from '../button-icon/ButtonIcon.vue'

export default {
  components: { ButtonIcon },
  props: {
    id: Number,
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
  }
}
</script>

<template>
  <div class="todo-item__wrapper" :class="isCompleted ? 'completed' : ''">
    <div class="title">
      <div class="btn-check">
        <input type="checkbox" :checked="isCompleted" v-model="isCompleted"/>
      </div>

      <p>
        {{ label }}
      </p>

      <ButtonIcon icon="more_vert" />
    </div>

    <div v-if="description" class="description">
      <p>
        {{ description }}
      </p>
    </div>
  </div>
</template>
