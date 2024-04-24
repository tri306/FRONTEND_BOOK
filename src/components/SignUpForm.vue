<script>
import { useUserStore } from '@/stores/user';
import { ElMessage } from 'element-plus';

const user = useUserStore();

export default {
    components: {},
    data: () => {
        return {
            Holot: '',
            Ten: '',
            GioiTinh: '',
            DiaChi: '',
            SoDienThoai: '',
            password: '',
            rePassword: '',
            message: '',
            // Image: '',
            // imagePreviewUrl: '',
        };
    },
    computed: {
        userAvatar() {
            return useUserStore().Image;
        },
    },
    methods: {
        handleImageUpload(event) {
            const file = event.target.files[0];
            this.uploadImage(file);
        },
        uploadImage(file) {
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = () => {
                this.Image = reader.result; // Sửa lưu trữ đường dẫn hình ảnh
                this.imagePreviewUrl = reader.result; // Lưu trữ đường dẫn hình ảnh xem trước
            };
            reader.onerror = () => {
                console.error('Error occurred while reading the file.');
            };
        },
        submit: async function () {
            if (
                this.password == this.rePassword &&
                this.password &&
                this.SoDienThoai &&
                this.Holot &&
                this.DiaChi &&
                this.GioiTinh
                // this.Image
            ) {
                this.message = await user.SignUp({
                    Holot: this.Holot,
                    Ten: this.Ten,
                    GioiTinh: this.GioiTinh,
                    DiaChi: this.DiaChi,
                    SoDienThoai: this.SoDienThoai,
                    password: this.password,
                    // Image: this.Image,
                });

                // this.$emit('handleSubmit', {
                //     Holot: this.Holot,
                //     Ten: this.Ten,
                //     GioiTinh: this.GioiTinh,
                //     DiaChi: this.DiaChi,
                //     SoDienThoai: this.SoDienThoai,
                //     password: this.password,
                // });
            } else {
                this.message = 'Mật khẩu xác thực không chính xác';
            }
            ElMessage(this.message);
        },
    },
};
</script>

<template>
    <div class="container flex justify-center items-center h-full">
        <div class="shadow-xl flex justify-center items-center flex-col p-8 rounded-md">
            <div class="flex justify-center">
                <div><h2>Tạo tài khoản</h2></div>
                <router-link to="/">
                    <div class="flex justify-center">
                        <!-- <img src="../assets/img/logo.png" class="justify-center items-center" /> -->
                    </div>
                </router-link>
            </div>
            <div class="grid gap-1">

                <input
                    type="text"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-4"
                    placeholder="Số điện thoại"
                    v-model="SoDienThoai"
                />
                <input
                    type="password"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-3"
                    placeholder="Mật khẩu"
                    v-model="password"
                />
                <input
                    type="password"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-3"
                    placeholder="Mật khẩu xác thực"
                    v-model="rePassword"
                />
                <input
                    type="text"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-3"
                    placeholder="Họ"
                    v-model="Holot"
                />
                <input
                    type="text"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-3"
                    placeholder="Tên"
                    v-model="Ten"
                />
                <input
                    type="text"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-3"
                    placeholder="Giới tính"
                    v-model="GioiTinh"
                />
                <input
                    type="text"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white mt-3"
                    placeholder="Địa chỉ"
                    v-model="DiaChi"
                />
                <div class="d-flex flex-column my-2" style="width: 300px">
                    <label for="imageUpload" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                        >Tải lên ảnh:</label
                    >
                    <input
                        type="file"
                        id="imageUpload"
                        @change="handleImageUpload"
                        accept="image/*"
                        class="block w-full text-sm text-gray-900 border border-gray-300 rounded-lg cursor-pointer bg-gray-50 dark:text-gray-400 focus:outline-none dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400"
                    />
                    <p class="text-sm text-gray-500 dark:text-gray-300">
                        
                    </p>
                    <div v-if="imagePreviewUrl">
                        <img :src="imagePreviewUrl" alt="Preview" style="max-width: 100%; max-height: 200px" />
                    </div>
                </div>
            </div>
            <button
                type="button"
                class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                @click="submit"
            >
                Đăng ký
            </button>
            <span class="mt-2"
                >Nếu đã có tài khoản?
                <router-link to="/login"><span class="text-blue-700">Đăng nhập</span></router-link></span
            >
        </div>
    </div>
</template>
