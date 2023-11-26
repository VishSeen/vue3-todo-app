<script>
    import './style.scss';
    import DropdownItem from '../dropdown-item/DropdownItem.vue';

    export default {
        name: "DropDown",
        components: { DropdownItem },
        props: {
            items: Array
        }
    }
</script>


<template>
    <div class="dropdown">
        <li v-for="item in items" :key="item.id">
                <DropdownItem :label="item.label" @click="item.clickEvent(item.label)"/>
            </li>
    </div>
</template>