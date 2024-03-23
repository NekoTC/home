<template>
  <div v-if="siteLinks[0]" class="links">
    <div class="line">
      <Icon size="20">
        <Link />
      </Icon>
      <span class="title">网站列表</span>
    </div>
      <!-- 友链 -->
      <div class="clear" id="links">
        <div class="links">
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
import { Icon } from "@vicons/utils";
// 可前往 https://www.xicons.org 自行挑选并在此处引入
import { Link, Blog, CompactDisc, Cloud, Compass, Book, Fire, LaptopCode } from "@vicons/fa"; // 注意使用正确的类别
import { mainStore } from "@/store";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination, Mousewheel } from "swiper";
import siteLinks from "@/assets/siteLinks.json";

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
/* 这里可以继续添加你的样式 */
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
[class*=" icon-"]:before,
[class^=icon-]:before {
  font-family: nekotora;
  font-style: normal;
  font-weight: 400;
  speak: none;
  display: inline-block;
  text-decoration: inherit;
  width: 1em;
  margin-right: .2em;
  text-align: center;
  font-variant: normal;
  text-transform: none;
  line-height: 1em;
  margin-left: .2em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale
}

.icon-search:before {
  content: "\e800"
}

.icon-info:before {
  content: "\e801"
}

.icon-comment:before {
  content: "\e802"
}

.icon-v2ex:before {
  content: "\e803"
}

.icon-zhihu:before {
  content: "\e804"
}

.icon-bilibili:before {
  content: "\e805"
}

.icon-netease_music:before {
  content: "\e806"
}

.icon-tencent_qzone:before {
  content: "\e807"
}

.icon-mail:before {
  content: "\e808"
}

.icon-bookmark:before {
  content: "\e809"
}

.icon-link:before {
  content: "\e80a"
}

.icon-twitter:before {
  content: "\f099"
}

.icon-gplus:before {
  content: "\f0d5"
}

.icon-github:before {
  content: "\f113"
}

.icon-unlink:before {
  content: "\f127"
}

.icon-instagram:before {
  content: "\f16d"
}

.icon-weibo:before {
  content: "\f18a"
}

.icon-qq:before {
  content: "\f1d6"
}

</style>
