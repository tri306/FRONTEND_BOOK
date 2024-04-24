<script>
import { ElMessage } from 'element-plus';
import BookForm from './BookForm.vue';
import { useBookStore } from '@/stores/book';

export default {
    props: {
        masach: {
            type: String,
            required: true,
        },
    },

    components: {
        BookForm,
    },

    data() {
        const book = useBookStore().getBook(this.masach);
        return {
            data: {
                ...book,
                manxb: book.manxb._id,
                namxuatban: new Date(book.namxuatban).getFullYear(),
            },
        };
    },
    methods: {
        async submit(data) {
            const result = await useBookStore().updateBook(data);
            ElMessage(result);
        },
    },
};
</script>

<template>
    <div>
        <!-- <ElAlert title="Cập nhật thành công" type="success" center show-icon class="m-4" /> -->
        <h4 class="m-4 text-center">Update book</h4>
        <BookForm :book="data" @handleSubmit="submit" />
    </div>
</template>

<style lang="scss"></style>
