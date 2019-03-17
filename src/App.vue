<template>
    <div id="app">
        <vheader :seller="seller"></vheader>
        <div class="tab border-1px">
            <div class="tab-item">
                <router-link to="/seller">商品</router-link>
            </div>
            <div class="tab-item">
                <router-link to="/goods">评论</router-link>
            </div>
            <div class="tab-item">
                <router-link to="/ratings">商家</router-link>
            </div>
        </div>
        <router-view></router-view>
    </div>
</template>

<script>
    import vheader from './components/header/index';

    const ERR_OK = 0;

    export default {
        name: 'App',
        components: {
            vheader
        },
        data() {
            return {
                seller: {}
            }
        },
        mounted() {
            this.axios.get('/api/seller').then((response) => {
                if (response.data.errno === ERR_OK) {
                    this.seller = response.data.data;
                }
                // 输出数据
                console.log('222', this.seller);
            })
        }
    }
</script>

<style lang="stylus">
    @import "common/stylus/mixin.styl"
    .tab
        display: flex
        width: 100%
        height: 40px
        line-height: 40px

        .tab-item
            flex: 1
            text-align: center
            // border-bottom: 1px solid rgba(7, 17, 27, .1)
            border-1px(rgba(7, 17, 27, .1))

            & > a
                display: block
                font-size: 14px
                color: rgb(77, 85, 93)

                &.active
                    color: rgb(240, 20, 20)
</style>
