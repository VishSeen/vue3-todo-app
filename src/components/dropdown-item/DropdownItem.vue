<script>
import './style.scss'

export default {
    props: {
        label: String,
        clickEvent: Function
    }
}
</script>

<template>
    <div class="dropdown-item">
        <button @click="$emit(this.label)">{{ label }}</button>
    </div>
</template>