<template>
    <div>
        <div class="my-tag">
            <input
                v-if="visable"
                v-focus
                ref="tagInput"
                class="input"
                type="text"
                placeholder="输入标签"
                @change="handleChange"
                @blur="visable = false"
                @keyup.enter="handleChange"
            />
            <div v-else class="text" @dblclick="handleClick">
                {{ item.tag }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        item: Object,
    },
    data() {
        return {
            visable: false,
        };
    },
    methods: {
        handleClick() {
            this.visable = true;
            // this.$nextTick(() => {
            //     this.$refs.tagInput.focus();
            // });
        },
        handleChange(e) {
            const item = { ...this.item, tag: e.target.value };
            this.visable = false;
            this.$emit("change", item);
        },
    },
};
</script>

<style lang="less" scoped>
.my-tag {
    cursor: pointer;
    .input {
        appearance: none;
        outline: none;
        border: 1px solid #ccc;
        width: 100px;
        height: 40px;
        box-sizing: border-box;
        padding: 10px;
        color: #666;
        &::placeholder {
            color: #666;
        }
    }
}
</style>
