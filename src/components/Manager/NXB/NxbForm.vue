<script>
export default {
    components: {},
    props: {
        nxb: {
            type: Object,
            required: false,
        },
    },
    data: () => {},
    methods: {
        submit() {
            this.$emit('handleSubmit', this.nxb);
        },
    },
};
</script>

<template>
    <div class="nxb">
        <div class="d-flex flex-column">
            <label>Tên NXB:</label>
            <el-input v-model="nxb.TenNxb" style="width: 300px" size="large" placeholder="Nhập tên nhà xuất bản" />
        </div>
        <div class="d-flex flex-column my-4">
            <label>Địa chỉ:</label>
            <el-input v-model="nxb.Diachi" style="width: 300px" size="large" placeholder="Nhập địa chỉ nhà xuất bản" />
        </div>
        <div class="d-flex justify-content-center align-items-center">
            <el-button type="success" plain @click="submit">Lưu NXB</el-button>
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
