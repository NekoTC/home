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
            <el-col v-for="(link, index) in site" :span="8" :key="link.id">
              <div
                class="item cards"
                :style="[index < 3 ? { marginBottom: '20px' } : null]"
                @click="visitLink(link.url)"
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
import axios from 'axios';

export default {
  data() {
    return {
      loading: true,
      site: [] // 存储友链数据
    };
  },
  created() {
    this.fetchLinks();
  },
  methods: {
    fetchLinks() {
      axios.get('https://mxapi.nekotc.cn/api/v2/links/all')
        .then(response => {
          // 在这里处理返回的 JSON 数据
          this.site = response.data.data; // 将获取到的数据保存到组件的数据中
          this.loading = false; // 设置加载状态为完成
        })
        .catch(error => {
          console.error('发生错误:', error);
        });
    },
    visitLink(url) {
      // 处理点击链接事件
      window.open(url, '_blank');
    }
  }
};
</script>

<style lang="scss" scoped>
@import url('src/components/css/h.9c69ed6c.css');
@import url('src/components/css/nekotora.99cf6f8c.css');
@import url('src/style/style.scss');
</style>
