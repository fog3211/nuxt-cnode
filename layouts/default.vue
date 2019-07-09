<template>
  <div>
    <header class="header">
      <a href="/" class="nav">全部</a>
      <nuxt-link
        v-for="item in tabs"
        :key="item.path"
        :to="'/?tab=' + item.path"
        class="nav"
        >{{ item.name }}</nuxt-link
      >
    </header>
    <nuxt />
    <footer class="footer">
      <p>Copyright © 2019 By Fog3211</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tabs: [
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
      ]
    };
  }
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
}
.header {
  background-color: #444;
  height: 50px;
  line-height: 50px;
  .nav {
    padding: 10px 15px;
    color: aliceblue;
    &:hover {
      background-color: #555;
    }
    &:active {
      color: rgb(213, 219, 224);
    }
  }
}
.footer {
  text-align: center;
  margin: 20px auto;
  color: rgb(46, 43, 43);
  font-style: italic;
  font-size: 14px;
}
</style>
