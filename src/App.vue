<script setup>
import SearchBar from './components/search-bar/SearchBar.vue'
import ButtonFab from './components/button-fab/ButtonFab.vue'
import PageTitle from './components/page-title/PageTitle.vue'
import ButtonIcon from './components/button-icon/ButtonIcon.vue';
</script>


<template>
    <div class="top-bar">
        <div class="left-side">
            <PageTitle title="Todo"/>
        </div>

        <div class="right-side">
            <SearchBar />
            <ButtonIcon
                icon="filter_alt"
                @click="console.log('Clicked')"
                outlined="true"
            />
        </div>
    </div>

    <ButtonFab />
</template>

