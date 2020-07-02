<template>
  <div>
    <Banner :banners="banners" :duration="3000" />
    <Channels @change="handleChange" />
    <Loading v-show="isLoading"/>
    <NewsList v-show="!isLoading" :news="news" />
  </div>
</template>

<script>
import Banner from "../components/Banner";
import Channels from "../components/news/Channels";
import NewsList from "../components/news/NewsList";
import Loading from "../components/Loading";
import { getNews } from "../services/newsService";
export default {
  components: {
    Banner,
    Channels,
    NewsList,
    Loading,
  },
  data() {
    return {
      banners: [
        {
          link: "https://s.weibo.com/top/summary?cate=realtimehot",
          url: require("../assets/banner/banner1.jpeg"),
        },
        {
          link: "https://www.electrotest.cn/zh-cn/activities/_.html",
          url: require("../assets/banner/banner2.jpeg"),
        },
        {
          link: "https://baijiahao.baidu.com/s?id=1659503970614293576&wfr=spider&for=pc",
          url: require("../assets/banner/banner3.jpeg"),
        },
      ],
      news: [],
      isLoading: true
    };
  },
  methods: {
    async handleChange(channelId) {
      this.isLoading = true;
      var resp = await getNews(channelId, 1, 10); //经过一段时间
      this.news = resp.contentlist;
      this.isLoading = false;
    },
  },
};
</script>

<style></style>
