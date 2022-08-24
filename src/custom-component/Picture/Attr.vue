<!-- eslint-disable vuejs-accessibility/form-control-has-label -->
<template>
    <div class="attr-list">
        <CommonAttr></CommonAttr>
        <el-form>
            <el-form-item label="镜像翻转">
                <div style="clear: both;">
                    <el-checkbox v-model="curComponent.propValue.flip.horizontal" label="horizontal">水平翻转</el-checkbox>
                    <el-checkbox v-model="curComponent.propValue.flip.vertical" label="vertical">垂直翻转</el-checkbox>
                </div>
            </el-form-item>
        </el-form>
        <label for="input" class="insert">
            <p style="opacity: 0.7;font-size:14px">插入图片</p>
            <input
                id="input"
                type="file"
                hidden
                @change="handleFileChange"
            />
        </label>
    </div>
</template>

<script>
import CommonAttr from '@/custom-component/common/CommonAttr.vue'

export default {
    components: { CommonAttr },
    props: {
        url: {
            type: String,
            default: '',
        },
    },
    data() {
        return {

        }
    },
    computed: {
        curComponent() {
            return this.$store.state.curComponent
        },
    },
    methods: {
        handleFileChange(e) {
            const file = e.target.files[0]
            if (!file.type.includes('image')) {
                // eslint-disable-next-line no-undef
                toast('只能插入图片')
                return
            }

            const reader = new FileReader()
            reader.onload = (res) => {
                const fileResult = res.target.result
                const img = new Image()
                img.onload = () => {
                    this.$store.commit('addComponent', {
                        component: {
                            ...CommonAttr,
                            // eslint-disable-next-line no-undef
                            id: generateID(),
                            component: 'Picture',
                            label: '图片',
                            icon: '',
                            propValue: {
                                url: fileResult,
                                flip: {
                                    horizontal: false,
                                    vertical: false,
                                },
                            },
                            style: {
                                // eslint-disable-next-line no-undef
                                ...commonStyle,
                                top: 0,
                                left: 0,
                                width: img.width,
                                height: img.height,
                            },
                        },
                    })

                    this.$store.commit('recordSnapshot')

                    // 修复重复上传同一文件，@change 不触发的问题
                    // eslint-disable-next-line no-undef
                    $('#input').setAttribute('type', 'text')
                    // eslint-disable-next-line no-undef
                    $('#input').setAttribute('type', 'file')
                }

                img.src = fileResult
            }

            reader.readAsDataURL(file)
        },
    },
}
</script>
