<template>
  <div class="gate ch">
    <div class="container links">
      <h2 class="chtitle">我的
        <span>好朋友</span>们</h2>
    <div class="clear" id="links">
      <div v-if="loading">加载中...</div>
      <div v-else>
        <div v-for="link in links" :key="link.id" class="item">
          <a :href="link.url" target="_blank">
            <div class="avatar"><img :src="link.avatar"></div>
            <div class="inner">
             <h5>{{ link.name }}</h5>
             <p>{{ link.description }}</p>
           </div>
          </a>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      loading: true,
      links: []
    };
  },
  mounted() {
    this.fetchLinks();
  },
  methods: {
    fetchLinks() {
      axios.get('https://mxapi.nekotc.cn/api/v2/links/all')
        .then(response => {
          if (response.status === 200) {
            this.links = response.data.data;
            this.loading = false;
          } else {
            console.error('请求友链失败' + response.status);
          }
        })
        .catch(error => {
          console.error('请求友链失败', error);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
@import url('src/components/css/h.9c69ed6c.css');
@import url('src/components/css/nekotora.99cf6f8c.css');
@import url('src/style/style.scss');
</style>
