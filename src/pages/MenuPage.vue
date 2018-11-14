<template>
  <v-ons-page>
    <v-ons-toolbar modifier="transparent" style="background:#146eb4;"></v-ons-toolbar>
    <div class="header">
      <img src="../assets/logo.png" alt="meshi-logo">
    </div>
    <div class="sidenav__msg">
      <div class="sidenav__msg__title">
        <p>このアプリの使い所</p>
      </div>
      <p>今日の晩ご飯が決められない時や精神的に疲れている時に使えるよ！</p>
    </div>
    <div class="sidenav__msg">
      <div class="sidenav__msg__title">
        <p>使用方法</p>
      </div>
      <p>1. 自分がよく行くお店や食べる料理をリストアップしてね。</p>
      <p>2. 「今日のメシを決める！」を押すとあなたの晩ご飯をランダムに決めてくれるよ♪</p>
    </div>
    <div class="sidenav__msg">
      <div class="sidenav__msg__title">
        <p>ちなみに...</p>
      </div>
      <p>スマホの方が使いやすいよ♪　気に入った人は「ホーム画面に追加」してね♪</p>
    </div>
    <v-ons-list-title style="margin-right:10px; text-align:right; color:white">@duuun02</v-ons-list-title>
    
  </v-ons-page>
</template>

<script>
import HomePage from "./HomePage";

export default {
  name: "menu",
  data() {
    return {
      essentialLinks: [
        {
          label: "Home",
          link: "/",
          icon: "fa-home"
        },
        {
          label: "このサイトについて",
          link: "/about",
          icon: "fa-info"
        }
      ]
    };
  },
  methods: {
    goTo(url) {
      const newWindow = window.open(url);
      newWindow.opener = null;
      newWindow.location = url;
    }
  }
};
</script>

<style scoped>
.header {
  text-align: center;
  margin-top: 40px;
}
img {
  max-width: 150px;
}
ons-list-title {
  text-transform: none;
}
ons-list-item {
  cursor: pointer;
}
.sidenav__msg {
  margin: 10px;
  color: #fff;
  font-family: "Kosugi maru", sans-serif;
}
.sidenav__msg__title {
  font-weight: bold;
  margin-left: 10px;
  font-family: "Kosugi maru", sans-serif;
}
.sidenav__msg__list {
  list-style-type: none;
}
</style>
