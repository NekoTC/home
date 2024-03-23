<template>
  <div class="gate ch">
    <h2>我的<span>好朋友</span>们</h2>
      <!-- 友链 -->
      <div class="clear" id="links">
        <div class="links">
          <div class="link-all">
            <div v-if="loading">加载中...</div>
            <div v-else>
              <div v-for="link in links" :key="link.id" class="item">
                <a :href="link.url" target="_blank">
                  <div class="avatar centered"><img :src="link.avatar" width="64" height="64"></div>
                  <div class="item">
                    <h5 class="name centered">{{ link.name }}</h5>
                    <p class="centered">{{ link.description }}</p>
                  </div>
                </a>
              </div>
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

<style lang="scss" scoped>
.link-all {
  height: 220px;
  .item {
    height: 100px;
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: row;
    justify-content: center;
    padding: 0 10px;
    animation: fade 0.5s;
  }
}
@import url('src/components/css/h.9c69ed6c.css');
@import url('src/components/css/nekotora.99cf6f8c.css');
</style>
