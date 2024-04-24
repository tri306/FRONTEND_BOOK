<script>
import { nxbStore } from '@/stores/nxb';
const nxb = nxbStore();
const open2 = () => {
    ElMessage({
        message: 'Congrats, this is a success message.',
        type: 'success',
    });
};
export default {
    components: {},
    props: {
        book: {
            type: Object,
            required: false,
        },
    },
    data: () => {
        return {
            nxbs: nxb.NXB,
        };
    },
    methods: {
        submit() {
            this.$emit('handleSubmit', this.book);
        },
        handleImageUpload(event) {
            const file = event.target.files[0];
            this.uploadImage(file);
        },
        uploadImage(file) {
            // Tạo đối tượng FileReader để đọc tệp hình ảnh
            const reader = new FileReader();

            // Đọc dữ liệu hình ảnh
            reader.readAsDataURL(file);

            // Xử lý khi dữ liệu được đọc
            reader.onload = () => {
                // Lưu trữ đường dẫn hình ảnh được tải lên
                this.book.image = reader.result;
            };

            // Xử lý khi có lỗi xảy ra
            reader.onerror = () => {
                console.error('Error occurred while reading the file.');
            };
        },
    },
};
</script>

<template>
    <div class="nxb">
        <div class="d-flex flex-column">
            <label>Tên sách:</label>
            <el-input v-model="book.tensach" style="width: 300px" size="large" placeholder="Tên quyển sách" />
        </div>
        <div class="d-flex flex-column my-2">
            <label>Số tiền (VND):</label>
            <el-input
                v-model="book.dongia"
                type="number"
                style="width: 300px"
                size="large"
                placeholder="Nhập giá tiền (VND)"
            />
        </div>
        <div class="d-flex flex-column my-2">
            <label>Số lượng:</label>
            <el-input v-model="book.soquyen" style="width: 300px" size="large" placeholder="Nhập số lượng" />
        </div>
        <div class="d-flex flex-column my-2" style="width: 300px">
            <label>NXB:</label>
            <el-select
                class="w-100"
                v-model="book.manxb"
                placeholder="Thay đổi NXB"
                size="large"
                style="width: 240px"
            >
                <el-option v-for="nxb in nxbs" :key="nxb._id" :label="nxb.TenNxb" :value="nxb._id" />
            </el-select>
        </div>
        <div class="d-flex flex-column my-2">
            <label>Năm sản xuất:</label>
            <el-input
                v-model="book.namxuatban"
                type="number"
                style="width: 300px"
                size="large"
                placeholder="Nhập năm xuất bản"
            />
        </div>
        <div class="d-flex flex-column my-2">
            <label>Tác giả:</label>
            <el-input v-model="book.tacgia" style="width: 300px" size="large" placeholder="Nhập tên tác giả" />
        </div>
        <div class="d-flex flex-column my-2" style="width: 300px">
            <label>Hình ảnh:</label>
            <el-input v-model="book.image" style="width: 300px" size="large" placeholder="Nhập Link ảnh" />
        </div>
        <div class="d-flex flex-column my-2" style="width: 300px">
            <label for="imageUpload">Tải lên ảnh:</label>
            <input type="file" id="imageUpload" @change="handleImageUpload" accept="image/*" style="width: 300px" />
            <div v-if="imagePreviewUrl">
                <img :src="imagePreviewUrl" alt="Preview" style="max-width: 100%; max-height: 200px" />
            </div>
        </div>
        <div class="d-flex flex-column my-2" style="width: 300px">
            <label for="imageUpload" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Ảnh bìa:</label
            >
            <input
                type="file"
                id="imageUpload"
                @change="handleImageUpload"
                accept="image/*"
                class="block w-full text-sm text-gray-900 border border-gray-300 rounded-lg cursor-pointer bg-gray-50 dark:text-gray-400 focus:outline-none dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400"
            />
            <p class="mt-1 text-sm text-gray-500 dark:text-gray-300">
                <!-- Chỉ hỗ trợ các định dạng ảnh (PNG, JPG, GIF) với kích thước tối đa 800x400px. -->
            </p>
            <div v-if="imagePreviewUrl">
                <img :src="imagePreviewUrl" alt="Preview" style="max-width: 100%; max-height: 200px" />
            </div>
        </div>

        <div class="d-flex justify-content-center align-items-center">
            <el-button type="success" plain @click="submit">Lưu thông tin sách</el-button>
        </div>
    </div>
</template>

<style lang="scss">
.nxb {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
</style>
