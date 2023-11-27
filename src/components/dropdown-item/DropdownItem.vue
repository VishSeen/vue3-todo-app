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
        <button @click="this.clickEvent">{{ label }}</button>
    </div>
</template>