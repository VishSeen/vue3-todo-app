<script>
import './style.scss';

export default {
    name: "TodoHeader",
    props: {
        title: String,
        count: Number,
        type: String
    }
}
</script>

<template>
    <div class="todo-header" :class="type">
        <div class="title">
            <div class="circle"></div>
            <p>{{ title }}</p>
        </div>

        <div class="ic-count">
            <span>
                {{ count }}
            </span>
        </div>
    </div>
</template>