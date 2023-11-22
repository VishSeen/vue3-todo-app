<script>
    import './style.scss';

    export default {
        props: {
            icon: String,
            outlined: Boolean,
            clickEvent: Event
        }
    }
</script>

<template>
    <button @click="clickEvent" class="btn-icon" :class="outlined ? 'outlined': ' '">
        <span class="material-symbols-outlined">
            {{ icon }}
        </span>
    </button>
</template>
