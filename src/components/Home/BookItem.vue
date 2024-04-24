<script>
export default {
    name: 'BookItem',
    props: {
        data: {
            type: Object,
            required: true,
        },
    },
    methods: {
        handleNavigate() {
            this.$router.push({
                name: 'book',
                params: {
                    id: data.masach,
                },
            });
        },
    },
};
</script>

<template>
    <div class="BookItem m-2 border-2 border-violet-500">
        <img :src="data.image" alt="" class="image" />
        <div class="flex justify-between items-center p-1">
            <div class="flex flex-col items-start justify-center">
                <h5 class="w-full">
                    <router-link :to="`/book/${data.masach}`" class="text-violet-600 text-decoration-none">
                        {{ data.tensach }}
                    </router-link>
                </h5>
                <span class="text-sm text-blue-600 overflow-hidden overflow-ellipsis line-clamp-1">
                    Tác giả: {{
                    data.tacgia
                }}</span>
                <p class="text-sm mt-0 text-orange-500">
                    Đơn giá: <span class="text-orange-500 font-semibold text-base">{{ data.dongia }} Đồng</span>
                </p>
    
                <p class="text-sm mt-0">
                    Còn lại: 
                    <span class="font-semibold text-base">{{ data?.soquyen - data?.soquyendamuon || 0 }}</span>
                </p>
            </div>
            
        </div>
        
    </div>
</template>

<style lang="scss">
.BookItem {
    box-shadow: rgba(0, 0, 0, 0.05) 0px 6px 24px 0px, rgba(0, 0, 0, 0.08) 0px 0px 0px 1px;
    height: auto;
    max-width: auto;
    display: flex;
    flex-direction: column;

    .image {
        width: auto;
        height: 290px;
    }
}
.router-link-exact-active {
    text-decoration: none; /* Loại bỏ gạch chân */
}
</style>
