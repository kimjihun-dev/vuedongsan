<template>
    <section class="room">
        <ul class="rGnb">
            <li v-for="(item, index) in products" :key="index">
                <img :src='item.image'>
                <h4 @click="$emit('openModal', index);">{{ item.title }}</h4>
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    name: 'Card',
    props: {
        products: Object,
    },
}
</script>

<style>
.rGnb {
    padding: 50px 0;
}
.rGnb li { margin-bottom: 25px; }
.rGnb h4 { cursor: pointer; }
</style>