<script>
import Header from '@/components/Header.vue';
import { ElButton } from 'element-plus';
import BookList from '@/components/Home/BookList.vue';
import Footer from '@/components/Footer.vue';

export default {
    name: 'Home',
    components: {
        ElButton,
        Header,
        BookList,
        Footer,
    },
};
</script>

<template>
    <Header></Header>
    <main class="container ">
        <h1 class="text-center text-black-400">Đây là contact </h1>
        <h2 class="text-center">Phát triển ứng dụng web</h2>
        
    </main>
    <Footer></Footer>
</template>

<style lang="scss">
main {
    .pagination {
        margin-top: 12px;
        display: flex;
        align-items: center;
        justify-content: flex-end;
    }
}
</style>
