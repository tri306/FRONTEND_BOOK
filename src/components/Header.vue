<script>
import { ElButton, ElInput, ElMessage } from 'element-plus';
import { useUserStore } from '@/stores/user';
import { mapStores } from 'pinia';
import { useBookStore } from '@/stores/book';

export default {
    components: {
        ElInput,
        ElButton,
    },
    data: () => {
        return {
            value: '',
            user: useUserStore(),
        };
    },
    computed: {
        ...mapStores(useBookStore),
    },

    methods: {
        signOut: (user) => {
            user.SignOut();
            ElMessage({
                message: 'Logout Successfully!',
                type: 'error', // Đặt kiểu là 'success'
            });
        },
    },
    computeds: {},
};
</script>

<template>
    <div class="header">
        <div class="header-box container">
            <div class="flex items-center justify-between">
                <router-link to="/" class="flex">
                    <img src="../assets/img/logo.png" class="h-8 mr-3 rounded-full" />
                    <p class="logo-text">BookStore</p>
                </router-link>
            </div>

            <input type="text" class="search-input" placeholder="Search book" v-model="bookStore.searchTitle" />
            <!-- <p class="text-8xl">Hello</p> -->
            <div>
                <div class="dropdown" v-if="!user.token">
                    <img
                        class="w-10 h-10 p-1 rounded-full ring-2 ring-gray-300 dark:ring-gray-500"
                        src="../assets/img/avartar1.jpg"
                        alt="Bordered avatar"
                        data-bs-toggle="dropdown"
                    />

                    <ul class="dropdown-menu" aria-labelledby="login-btn">
                        <li>
                            <router-link class="dropdown-item" to="/login">Người dùng</router-link>
                        </li>
                        <li>
                            <router-link class="dropdown-item" to="/loginmanager">Admin</router-link>
                        </li>
                    </ul>
                </div>
                <div v-if="user.token">
                    <el-dropdown size="large" type="primary">
                        <span class="menu-icon"
                            ><img src="../assets/img/logo.png" class="h-8 mr-3 rounded-full"
                        /></span>
                        <template #dropdown>
                            <el-dropdown-menu>
                                <el-dropdown-item>
                                    <router-link class="action-link" to="/history">Lịch sử mượn sách</router-link>
                                </el-dropdown-item>
                                <el-dropdown-item>
                                    <router-link class="action-link" to="/manager/borrow">Quản lý</router-link>
                                </el-dropdown-item>
                                <el-dropdown-item>
                                    <div @click="signOut(user)">Đăng xuất</div>
                                </el-dropdown-item>
                            </el-dropdown-menu>
                        </template>
                    </el-dropdown>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.header {
    position: sticky;
    padding: 0;
    top: 0;
    left: 0;
    right: 0;
    background: #1b4a8f;

    .header-box {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 8px 0;
        .logo {
            height: 2rem;
            margin-right: 0.75rem;
            border-radius: 50%;
        }
        .logo-text {
            float: right;
            color: #000;
            font-weight: 600;
            font-size: 1.5rem;
            line-height: 2rem;
            white-space: nowrap;
            align-self: center;
        }
        .text {
            color: aqua;
        }
        .search-input {
            width: 600px;
            margin-left: 10px;
            border: 2px solid rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            padding: 4px 8px;

            &:focus {
                outline: none;
                border: 2px solid rgba(61, 108, 185, 0.6);
                box-shadow: rgba(0, 224, 255, 0.1) 0px 6px 12px -2px, rgba(0, 224, 255, 0.1) 0px 3px 7px -3px;
            }
        }
        .menu-icon {
            font-size: 26px;
        }
        .action-link {
            text-decoration: none;
        }
    }
}
</style>
