<script>
import './style.scss'

export default {
    props: {
        icon: String,
        isClicked: Boolean
    },
    methods: {
        click() {
            this.$emit.openModal;
            this.rotate = !this.rotate;
        }
    }
}
</script>

<template>
    <button class="button-fab" @click="click" :class="isClicked ? 'rotate' : ''">
        <span class="material-symbols-outlined">
            {{ icon }}
        </span>
    </button>
</template>