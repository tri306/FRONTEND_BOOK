<script>
import Header from "@/components/Header.vue";
import { ElButton } from "element-plus";
import BookList from "@/components/Home/BookList.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "Home",
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
    <h2 class="text-center m-2">Phát triển ứng dụng web</h2>
    <div class="bg-white/30 ..."><img src="../assets/img/R.jpg" alt="" /></div>
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
