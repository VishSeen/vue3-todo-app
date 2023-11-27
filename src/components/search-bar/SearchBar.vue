<script>
import './style.scss';
import ButtonIcon from '../button-icon/ButtonIcon.vue';

export default {
    components: { ButtonIcon },
    props: {
        search: Function
    }
}
</script>

<template>
    <div class="search-bar__wrapper">
        <ButtonIcon icon="search"/>
        <input type="text" @change="this.$emit('search-change', $event.target.value)" placeholder="Search..." name="search">
    </div>
</template>
