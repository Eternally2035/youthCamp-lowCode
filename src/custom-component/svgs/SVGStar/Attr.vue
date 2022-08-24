<template>
    <div class="attr-list">
        <CommonAttr></CommonAttr>
        <el-form>
            <el-form-item label="内容">
                <el-input v-model="curComponent.propValue" type="textarea" :rows="3" />
            </el-form-item>
        </el-form>
        <el-form>
            <el-form-item label="链接">
                <el-input v-model="message" type="text">
                    {{ message }}
                </el-input>
                <el-button value="修改" @click="setM">跳转</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
import CommonAttr from '@/custom-component/common/CommonAttr.vue'

export default {
    components: { CommonAttr },
    data() {
        return {
            message: '默认地址',
            herf: '',
        }
    },
    computed: {
        curComponent() {
            return this.$store.state.curComponent
        },
    },
    methods: {
        setM() {
            // eslint-disable-next-line no-alert, no-sequences
            alert('正在跳转'),
            // eslint-disable-next-line no-restricted-globals
            window.location.replace('https://' + this.message)
        },
    },
}
</script>
