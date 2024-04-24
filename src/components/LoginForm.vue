<script>
import { useUserStore } from '@/stores/user';
export default {
    components: {},
    data: () => {
        return {
            SoDienThoai: '',
            password: '',
        };
    },
    computed: {
        userAvatar() {
            return useUserStore().Image;
        },
    },
    methods: {
        routeBookCheck() {
            return this.$router.currentRoute._value.name;
        },
        submit() {
            this.$emit('handleSubmit', {
                SoDienThoai: this.SoDienThoai,
                password: this.password,
            });
        },
    },
};
</script>

<template>
    <div class="container flex justify-center items-center h-full mt-16">
        <div
            class="w-full max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700"
        >
            <div class="space-y-6">
                <div class="flex justify-center">
                    <router-link to="/">
                        <div class="flex justify-center">
                            <!-- <img src="../assets/img/logo.png" class="justify-center items-center" /> -->
                            <img src="../assets/img/logo.png" class="justify-center items-center" />
                        </div>
                    </router-link>
                </div>
                <div>
                    <label for="SoDienThoai" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                        >Số điện thoại</label
                    >
                    <input
                        type="text"
                        id="SoDienThoai"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                        placeholder="Số điện thoại"
                        v-model="SoDienThoai"
                        required
                    />
                </div>
                <div>
                    <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                        >Mật khẩu</label
                    >
                    <input
                        type="password"
                        id="password"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                        placeholder="••••••••"
                        v-model="password"
                        required
                    />
                </div>
                <div class="flex items-start">
                    <div class="flex items-start">
                        <div class="flex items-center h-5">
                            <input
                                id="remember"
                                type="checkbox"
                                value=""
                                class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800"
                                required
                            />
                        </div>
                        <label for="remember" class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300"
                            >Remember me</label
                        >
                    </div>
                    <!-- <a href="#" class="ms-auto text-sm text-blue-700 hover:underline dark:text-blue-500"
                        >Lost Password?</a
                    > -->
                </div>
                <button
                    type="button"
                    class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                    @click="submit"
                >
                    Đăng Nhập
                </button>
                <div class="text-sm font-medium text-gray-500 dark:text-gray-300">
                    Bạn chưa có tài khoản?
                    <router-link to="/signup" class="text-blue-700 hover:underline dark:text-blue-500"
                        >Tạo tài khoản</router-link
                    >
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.container {
    justify-content: center;
    align-items: center;
}
</style>
