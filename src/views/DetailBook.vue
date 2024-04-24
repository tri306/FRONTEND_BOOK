<script>
import { ElButton, ElMessage } from 'element-plus';
import BookList from '@/components/Home/BookList.vue';
import { mapStores } from 'pinia';
import { useBookStore } from '@/stores/book';
import { useUserStore } from '@/stores/user';
import { useBorrowStore } from '@/stores/borrow';
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
export default {
    name: 'Home',
    props: {
        id: {
            type: String,
            required: true,
        },
    },
    components: {
        ElButton,
        BookList,
        Header,
        Footer,
    },
    computed: {
        ...mapStores(useBookStore, useUserStore, useBorrowStore),
    },
    data() {
        return {
            quantity: 0,
        };
    },
    methods: {
        handleChange(value) {
            this.quantity = value;
        },
        async handleBorrow() {
            if (!this.userStore.token) {
                ElMessage({
                    message: 'Vui lòng đăng nhập để mượn sách!',
                    type: 'error', // Đặt kiểu là 'success'
                });

                this.$router.push('/login');
                return;
            }
            const data = {
                masach: this.bookStore.getBook(this.id)._id,
            };
            const result = await this.borrowStore.borrowBook(data);
            ElMessage({
                message: result,
                type: 'error', // Đặt kiểu là 'success'
            });
        },
    },
};
</script>

<template>
    <Header></Header>
    <main class="container">
        <div class="detail-container mt-2">
            <div class="imageBox">
                <img class="image" :src="bookStore.getBook(id).image" alt="" />
            </div>
            <div class="detailInfor">
                <h4 class="text-red-600">{{ bookStore.getBook(id).tensach }}</h4>
                <p class="text-blue-500">Author: {{ bookStore.getBook(id).tacgia }}</p>

                <!-- <p class="pay">{{ bookStore.getBook(id).dongia }} đ</p> -->
                <div class="borrow-container">
                    <!-- <span class="borrow-quantity">Số lượng</span>
                    <el-input-number v-model="quantity" :min="1" :max="1" @change="handleChange" /> -->
                </div>
                <div class="mt-2">
                    <h6 class="title-description">Chi tiết sách:</h6>
                    <p class="detail">
                        Author: <span class="text-red-600">{{ bookStore.getBook(id).tacgia }}</span>
                    </p>
                    <p class="detail">
                        Publisher :<span class="text-red-600"> {{ bookStore.getBook(id).manxb.TenNxb }}</span>
                    </p>
                    <p class="detail">
                        Publishing year:
                        <span class="text-red-600">
                            {{ new Date(bookStore.getBook(id).namxuatban).getFullYear() }}</span
                        >
                    </p>
                </div>
                <p class="quantity">
                    Remaining:
                    <span class="text-red-600">{{
                        bookStore.getBook(id).soquyen - bookStore.getBook(id).soquyendamuon
                    }}</span>
                </p>
                <div class="">
                    <el-button type="danger" class="bg-red-600" plain @click="handleBorrow">Mượn sách</el-button>
                </div>
            </div>
        </div>
    </main>
    <Footer></Footer>
</template>

<style lang="scss">
main {
    .detail-container {
        padding: 16px;
        box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
        display: flex;
        flex-direction: row;

        .imageBox {
            margin-right: 16px;
            .image {
                max-width: 300px;
            }
        }

        .detailInfor {
            .title {
                margin-bottom: 0px;
            }
            .author {
                margin-top: 0;
                margin-bottom: 0px;
                color: #1d9d74;
            }
            .pay {
                font-size: 26px;
                color: #fe642e;
                font-weight: 600;
            }
            .quantity {
                span {
                    font-size: 24px;
                    font-weight: 600;
                }
            }
            .borrow-container {
                margin-top: 0px;
                .borrow-quantity {
                    margin-right: 8px;
                }
            }

            .title-description {
                margin-top: 0px;
            }
            .detail {
                margin: 2px;
            }
        }
    }
}
</style>
