<template>
  <div>
    <!-- 友链列表 -->
    <div class="clear" id="links">
      <div v-for="link in links" :key="link.id">
        <a :href="link.url" target="_blank">
          <div class="item">
            <div class="avatar"><img :src="link.avatar"></div>
            <div class="inner">
              <h5>{{ link.name }}</h5>
              <p>{{ link.description }}</p>
            </div>
          </div>
        </a>
      </div>
    </div>

    <!-- 友链列表 -->
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
      friends: [],
      links: []
    };
  },
  created() {
    this.fetchFriends();
    this.fetchLinks();
  },
  methods: {
    fetchFriends() {
      axios.get('https://mxapi.nekotc.cn/api/v2/links/all')
        .then(response => {
          // 请求成功，更新友链列表
          this.friends = response.data.data;
        })
        .catch(error => {
          // 请求失败，处理错误
          console.error('获取友链失败:', error);
        });
    },
    fetchLinks() {
      var xhr = new XMLHttpRequest();
      xhr.open('GET', 'https://mxapi.nekotc.cn/api/v2/links/all', true);
      xhr.setRequestHeader('Content-Type', 'application/json');

      xhr.onload = () => {
        if (xhr.status >= 200 && xhr.status < 300) {
          var data = JSON.parse(xhr.responseText);
          this.links = data.data;
        } else {
          console.error('请求友链失败' + xhr.status);
        }
      };

      xhr.send();
    }
  }
};
</script>
