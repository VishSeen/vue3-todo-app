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
        <button>{{ label }}</button>
    </div>
</template>