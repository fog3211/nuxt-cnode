<template>
  <div class="container">
    <div class="topic">
      <div class="main">
        <h2 class="title">
          {{ detail.title }}
        </h2>
        <div class="info">
          <img :src="detail.author.avatar_url" alt="img" class="avatar" />
          <span class="name">
            {{ detail.author.loginname }}
          </span>
          <span class="time">
            {{ formatTime(detail.create_at) }}
          </span>
        </div>
        <div class="content" v-html="detail.content"></div>
      </div>
    </div>

    <div class="comments">
      <div class="topic" v-for="item in detail.replies" :key="item.id">
        <div class="info">
          <img :src="item.author.avatar_url" alt="img" class="avatar" />
          <span class="name">
            {{ item.author.loginname }}
          </span>
        </div>
        <div class="content" v-html="item.content"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  asyncData({ params }) {
    // console.log(params);
    return axios
      .get("https://cnodejs.org/api/v1/topic/" + params.id)
      .then(res => {
        // console.log(res.data.data);
        return { detail: res.data.data };
      })
      .catch(err => {
        // console.log(err);
      });
  },
  data() {
    return {
      detail: {}
    };
  },
  methods: {
    formatTime(t) {
      return t.slice(0, 10);
    }
  }
};
</script>

<style lang="scss" scoped>
* {
  margin: 5px;
  line-height: 2;
}
.container {
  width: 90%;
  min-width: 320px;
  margin: 20px auto;
  padding: 10px;
  border: 1px solid #ccc;
  background-color: rgb(248, 245, 245);
  word-break: break-all;
  overflow: hidden;
  .topic {
    width: 100%;
    border-bottom: 1px solid #ccc;
    padding-bottom: 10px;
    .info {
      margin-top: 10px;
      .name {
        font-style: italic;
        color: rgb(161, 155, 155);
      }
    }
  }
  .avatar {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-size: cover;
    border: 1px solid #ccc;
    margin: 0 10px;
  }
  .time {
    float: right;
    margin-right: 10px;
  }
}
</style>

