<script>
import './style.scss';
import ButtonIcon from '../button-icon/ButtonIcon.vue';

export default {
    components: { ButtonIcon }
}
</script>

<template>
    <div class="search-bar__wrapper">
        <ButtonIcon icon="search"/>
        <input type="text" placeholder="Search..." name="search">
    </div>
</template>
