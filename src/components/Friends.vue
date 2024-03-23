<template>
  <div class="gate ch">
    <div class="container links">
      <h2 class="chtitle">我的<span>好朋友</span>们</h2>
      <!-- 友链 -->
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
      const xhr = new XMLHttpRequest();
      xhr.open('GET', 'https://mxapi.nekotc.cn/api/v2/links/all', true);
      xhr.setRequestHeader('Content-Type', 'application/json');

      xhr.onload = () => {
        if (xhr.status >= 200 && xhr.status < 300) {
          const data = JSON.parse(xhr.responseText);
          this.links = data.data;
          this.loading = false;
        } else {
          console.error('请求友链失败' + xhr.status);
        }
      };

      xhr.send();
    }
  }
};
</script>

<style>
/* 样式可以根据需要自行添加或修改 */
</style>