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
<!-- 友链 -->
<div class="clear" id="links">
<script>var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://rua.nekorua.com/api/v2/links/all', true);
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.onload = function() {
  if (xhr.status >= 200 && xhr.status < 300) {
    var data = JSON.parse(xhr.responseText);
    var links = data.data;

    var linksContainer = document.getElementById('links');
    links.forEach(function(link) {
      var linkElement = document.createElement('div');
      linkElement.innerHTML = `
						<a href="${link.url}" target="_blank">
							<div class="item">
								<div class="avatar"> <img src="${link.avatar}"> </div>
								<div class="inner">
									<h5>${link.name}</h5>
									<p>${link.description}</p>
								</div>
							</div>
						</a>`;
      linksContainer.appendChild(linkElement);
    });
  } else {
    console.error('请求友链失败' + xhr.status);
  }
};

xhr.send();</script>
</div>
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
  .swiper {
    left: -10px;
    width: calc(100% + 20px);
    padding: 5px 10px 0;
    z-index: 0;
    .swiper-slide {
      height: 100%;
    }
    .swiper-pagination {
      position: static;
      margin-top: 4px;
      :deep(.swiper-pagination-bullet) {
        background-color: #fff;
        width: 18px;
        height: 4px;
        border-radius: 4px;
        transition: opacity 0.3s;
        &:hover {
          opacity: 1;
        }
      }
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

      .name {
        font-size: 1.1rem;
        margin-left: 8px;
      }
      @media (min-width: 720px) and (max-width: 820px) {
        .name {
          display: none;
        }
      }
      @media (max-width: 720px) {
        height: 80px;
      }
      @media (max-width: 460px) {
        flex-direction: column;
        .name {
          font-size: 1rem;
          margin-left: 0;
          margin-top: 8px;
        }
      }
    }
    @media (max-width: 720px) {
      height: 180px;
    }
  }
}
</style>

