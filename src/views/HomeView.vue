<script>

import { ElButton } from 'element-plus';
import BookList from '@/components/Home/BookList.vue';
import Header from '@/components/Header.vue';
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
    <main class="container">
        <h3 class="text-center text-sky-400 m-2 py-12">Sách là nền tri thức của nhân loại.</h3>
        <BookList></BookList>
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
