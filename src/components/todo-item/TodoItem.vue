
<script>
export default {
    components: { ButtonIcon },
    props: {
        id: Number,
        label: String,
        isChecked: Boolean
    }
}
</script>


<template>
    <div class="todo-item">
        <div class="btn-check">

        </div>

        <p class="txt-label">
            {{ label }}
        </p>

        <div class="btn-edit">
            <ButtonIcon icon="more_vert" />
        </div>
    </div>
</template>