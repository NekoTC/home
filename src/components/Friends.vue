<template>
  <div class="gate ch">
    <div class="container links">
      <h2 class="chtitle">我的<span>好朋友</span>们</h2>
      <!-- 友链 -->
      <div class="clear" id="links">
        <div class="links">
          <div class="line">
            <div class="title">友情链接</div>
          </div>
          <div class="link-all">
            <div v-if="loading">加载中...</div>
            <div v-else>
              <div v-for="link in links" :key="link.id" class="item">
                <a :href="link.url" target="_blank">
                  <div class="avatar"><img :src="link.avatar" width="64" height="64"></div>
                  <div class="inner">
                    <h5 class="name">{{ link.name }}</h5>
                    <p>{{ link.description }}</p>
                  </div>
                </a>
              </div>
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
.links {
  .line {
    margin: 2rem 0.25rem 1rem;
    font-size: 1.1rem;
    display: flex;
    align-items: center;
    animation: fade 0.5s;
    .title {
      margin-left: 8px;
      font-size: 1.15rem;
      text-shadow: 0 0 5px #00000050;
    }
  }
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

      &:hover {
        transform: scale(1.02);
        background: rgb(0 0 0 / 40%);
        transition: 0.3s;
      }

      &:active {
        transform: scale(1);
      }

      .avatar img {
        width: 64px;
        height: 64px;
      }

      .name {
        font-size: 1.1rem;
        margin-left: 8px;
      }
    }
  }
}
</style>
