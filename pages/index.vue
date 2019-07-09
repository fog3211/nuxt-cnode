<template>
  <div class="container">
    <ul class="list">
      <li class="topic" v-for="item in list" :key="item.id">
        <div class="section">
          <h3>
            <nuxt-link
              :to="{ name: 'topic-id', params: { id: item.id } }"
              class="title"
              >{{ item.title }}</nuxt-link
            >
          </h3>
          <div class="info">
            <span v-if="item.top" class="label checked">置顶</span>
            <span v-else class="label unchecked">{{ tabsObj[item.tab] }}</span>
            <img :src="item.author.avatar_url" alt="avatar" class="avatar" />
            <span class="name">
              {{ item.author.loginname }}
            </span>
            <span class="time">
              {{ formatTime(item.create_at) }}
            </span>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

const tabs = [
  {
    name: "精华",
    path: "good"
  },
  {
    name: "问答",
    path: "ask"
  },
  {
    name: "招聘",
    path: "job"
  },
  {
    name: "分享",
    path: "share"
  }
];
let tabsObj = {};
tabs.map(tab => {
  tabsObj[tab.path] = tab.name;
});
export default {
  asyncData({ query }) {
    // console.log("query", query);
    return axios
      .get(`https://cnodejs.org/api/v1/topics?tab=${query.tab || ""}`)
      .then(res => {
        console.log(res.data.data);
        return { list: res.data.data };
      });
  },
  data() {
    return {
      tabs,
      tabsObj
    };
  },
  methods: {
    getData(tab) {
      axios
        .get(`https://cnodejs.org/api/v1/topics?tab=${tab || ""}`)
        .then(res => {
          console.log(res.data.data);
          this.list = res.data.data;
        });
    },
    formatTime(t) {
      return t.slice(0, 10);
    }
  },
  watch: {
    $route() {
      this.getData(this.$route.query.tab || "");
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  width: 90%;
  min-width: 320px;
  margin: 20px auto;
  padding: 10px;
  border: 1px solid #ccc;
  background-color: rgb(248, 245, 245);

  .topic {
    margin-top: 5px;
    border-bottom: 1px solid #ccc;
    // height: 70px;
    &:last-child {
      border-bottom: none;
    }
    .title {
      color: #000;
      overflow: hidden;
    }
    .info {
      display: block;
      margin-top: 8px;
      img {
        vertical-align: middle;
      }
      .label {
        font-size: 14px;
        padding: 2px 4px;
        color: #999;
      }
      .checked {
        background-color: #80bd01;
        color: #fff;
      }
      .unchecked {
        background-color: #e5e5e5;
      }

      .avatar {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        background-size: cover;
        border: 1px solid #ccc;
        margin: 0 10px;
      }

      .name {
        font-style: italic;
        color: rgb(161, 155, 155);
      }
      .time {
        float: right;
        margin-right: 10px;
      }
    }
  }
}
</style>
