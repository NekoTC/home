<template>
  <div class="gate ch">
    <div class="container links">
      <span class="title">文章</span>
      <div class="clear" id="links">
        <div v-if="loading">加载中...</div>
        <div v-else>
          <div v-for="(link, index) in links.slice(0, 4)" :key="link.id" class="item">
            <a :href="`https://blog.nekotc.cn/posts/${link.category.slug}/${link.slug}`" target="_blank">
              <div class="inner">
                <h5>{{ link.title }}</h5>
                <p>{{ link.created }}</p>
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
      axios.get('https://mxapi.nekotc.cn/api/v2/posts')
        .then(response => {
          if (response.status === 200) {
            this.links = response.data.data;
            this.loading = false;
          } else {
            console.error('请求文章失败' + response.status);
          }
        })
        .catch(error => {
          console.error('请求文章失败', error);
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
