<template>
    <view class="content">
        <view class="uni-list">
            <view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" @tap="opennews" :data-postid="item.post_id">
                <view class="uni-media-list content_box" >
                    <image class="uni-media-list-logo" :src="item.author_avatar"></image>
                    <view class="uni-media-list-body" style="text-align: left;padding:0 15px;">
                        <view class="uni-media-list-text-top title_con" style="font-size:14px;">{{item.title}}</view>
                        <view class="uni-media-list-text-bottom uni-ellipsis" style="font-size: 12px;">{{item.created_at}}</view>
                    </view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                news: []
            };
        },
        onLoad:function(){
            uni.request({
                url: 'https://unidemo.dcloud.net.cn/api/news',
                method: 'GET',
                data: {},
                success: res => {
                    this.news = res.data;
                },
                fail: () => {},
                complete: () => {}
            });
        },
        methods:{
            opennews(e){
                uni.navigateTo({
                    url: '../news/news?postid='+e.currentTarget.dataset.postid
                });
            }
        }
    }
</script>

<style>
.uni-media-list-body{height: auto;}
.uni-media-list-text-top{line-height: 1.6em;}
.content_box{
	margin:0 12upx  10upx 12upx;
	text-align: center;;
}
.content_box image{
	height: 280upx;
}
.title_con{
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
</style>

