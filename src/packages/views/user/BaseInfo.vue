<template>
    <a-form :model="form.formState" :label-col="form.labelCol">
        <a-form-item v-for="(item,idx) in form.lists" :key="idx" :label="item.name">
            <a-input v-if="item.key !== 'describe'" v-model:value="form.formState[item.key]" />
            <a-textarea readonly v-else v-model:value="form.formState[item.key]"/>
        </a-form-item>
    </a-form>
</template>
<script>
import { defineComponent, reactive } from 'vue'
import { useStore } from 'vuex'

export default defineComponent({
    setup() {
        const lists = [
            {
                name: '用户名',
                key: 'username',
            },
            {
                name: '邮箱',
                key: 'email',
            },
            {
                name: '公司',
                key: 'company',
            },
            {
                name: '职业',
                key: 'job',
            },
            {
                name: '地址',
                key: 'address',
            },
            {
                name: '登录次数',
                key: 'login_number',
            },
            {
                name: '创建时间',
                key: 'createTime',
            },
            {
                name: '描述',
                key: 'describe',
            },
        ]
        const formState = {}
        lists.map((item)=>{
            formState[item.key] = '';
        })
        const store = useStore()
        const userinfo = store.getters['user/userinfo']
        const form = reactive({
            formState:{...userinfo},
            lists,
            labelCol: { style: { width: '100px' } },
            wrapperCol: { span: 14 },
        })
        return {
            form,
        }
    },
})
</script>
