<script>
 export default {
    name: "PageTitle",
    props: {
        title: String
    }
 }
</script>

<template>
    <div class="title__wrapper">
        <h1>{{ title }}</h1>
    </div>
</template>