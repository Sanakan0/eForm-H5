<template lang="pug">
    div(class="mine")
        div(align="center")
            img(
                class="logo"
                src="https://picture-1256456369.cos.ap-shanghai.myqcloud.com/logo.2e928116.png"
            )
        van-cell-group(class="userinfo")
            van-cell(
                v-if="id.length !== 0"
                :title="username"
                :value="userType"
                :label="idTag"
            )/
            van-cell(
                v-else
                title="请登录"
                label="苏州大学统一身份认证"
                @click="userAction"
            )/
            LoginSheet/
        van-cell-group(title="活动")
            van-cell(title="我发起的活动" is-link :to="{path: '/mine/event'}")
            van-cell(title="我报名的活动" is-link :to="{path: '/mine/participate'}")
            van-cell(title="我发布的问卷" is-link :to="{path: '/mine/qnaire'}")
            van-cell(title="我发布的匿名问卷" is-link :to="{path: '/mine/anonymous_qnaire'}")
            van-cell(title="我提交的答卷" is-link :to="{path: '/mine/answer'}")
        van-cell-group(title="其他")
            van-cell(title="关于我们" is-link :to="{name: 'about'}")
            van-cell(title="反馈意见" is-link :to="{name: 'feedback'}")
</template>

<script>
    import * as types from '../../store/mutation-types';
    import LoginSheet from '@/components/LoginSheet/';
    import {mapState} from "vuex";

    export default {
        name: "index",
        components: {LoginSheet},
        computed: {
            ...mapState(['username', 'id', 'userType', 'idTag'])
        },
        methods: {
            userAction() {
                if (this.username.length === 0 && this.id.length === 0) {
                    this.$store.commit(types.SHOW_LOGIN_SHEET, true);
                } else {
                    // this.$router.push({name: 'userinfo'});
                }
            }
        },
        mounted() {
            this.$store.commit(types.SET_ACTIVE_TAB, 1);
        }
    }
</script>

<style scoped>
    .logo {
        margin: 1rem;
        height: 5rem;
    }


</style>