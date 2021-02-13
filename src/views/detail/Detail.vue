<template>
    <div id="detail" name ="Detail">
        <detail-nav-bar></detail-nav-bar>
        <detail-swiper :top-images="topImages"></detail-swiper>
    </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavbar'
import DetailSwiper from './childComps/DetailSwiper'
import {getDetail, Goods} from '../../network/detail'
export default {
    name: "Detail",
    components:{
        DetailNavBar,
        DetailSwiper,
    },
    data(){
        return {
            iid: null,
            topImages: [],
            goods: null
        }
    },
    created(){
        this.iid = this.$route.params.iid;
        getDetail(this.iid).then(res => {
            //获取顶部轮播数据
            const data = res.result
            this.topImages = data.itemInfo.topImages

            //获取商品信息
            this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
        })
    }
    
}
</script>

<style scoped>

</style>
