<template>
  <div>
    <h1>友链列表</h1>
    <ul>
      <li v-for="friend in friends" :key="friend.id">
        <a :href="friend.url" target="_blank">
          <img :src="friend.avatar" alt="avatar" style="width: 50px; height: 50px;">
          {{ friend.name }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      friends: []
    };
  },
  created() {
    this.fetchFriends();
  },
  methods: {
    fetchFriends() {
      axios.get('https://mxapi.nekotc.cn/api/v2/friends')
        .then(response => {
          // 请求成功，更新友链列表
          this.friends = response.data.data;
        })
        .catch(error => {
          // 请求失败，处理错误
          console.error('获取友链失败:', error);
        });
    }
  }
};
</script>
<style lang="scss" scoped>
.more-content {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
  width: 100%;
  height: 100%;
}
</style>
