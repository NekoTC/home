<template>
  <div class="gate ch">
    <div class="line">
      <span class="title">朋友们</span>
    </div>
    <!-- 友链 -->
    <div class="clear" id="links">
      <div class="links">
        <div class="link-all">
          <div v-if="loading">加载中...</div>
          <el-row class="link-all" :gutter="20">
            <el-col v-for="(item, index) in site" :span="8" :key="item">
              <div
                class="item cards"
                :style="index < 3 ? 'margin-bottom: 20px' : null"
                @click="link.url"
              >
                <Icon size="32">
                  <component :is="link.avatar" />
                </Icon>
                <span class="name text-hidden">{{ link.name }}</span>
              </div>
            </el-col>
          </el-row>
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
@import url('src/components/css/h.9c69ed6c.css');
@import url('src/components/css/nekotora.99cf6f8c.css');
@import url('src/style/style.scss');
</style>