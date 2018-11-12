<template>
  <v-ons-page>
    <v-ons-toolbar class="home-toolbar">
      <div class="left">
        <v-ons-toolbar-button @click="$store.commit('splitter/toggle')">
          <v-ons-icon icon="fa-bars"></v-ons-icon>
        </v-ons-toolbar-button>
      </div>
      <div class="center">{{ msg }}</div>
    </v-ons-toolbar>

    <div class="header">
      <span>今日のメシは...</span>
      <v-ons-card id="food" style="margin: 10px 50px;">？</v-ons-card>
      <v-ons-button modifier="material large" @click="getFood" style="width: 70%;">決める！！</v-ons-button>
    </div>

    <v-ons-list-title>メシリスト</v-ons-list-title>
    <v-ons-list>
      <v-ons-list-item v-for="item in list" :key="item.link">
        <div class="right" @click="close"><v-ons-icon fixed-width icon="fa-close"></v-ons-icon></div>
        <div class="center">{{ item.label }}</div>
      </v-ons-list-item>
    </v-ons-list>

    <v-ons-list-title>メシリスト</v-ons-list-title>
    <v-ons-row>
      <v-ons-col width="50%" v-for="item in list" :key="item.link">
        <v-ons-card>{{ item.label }}</v-ons-card>
      </v-ons-col>
    </v-ons-row>

    <!--
    <v-ons-list-title>Vue.js Ecosystem</v-ons-list-title>
    <v-ons-row>
      <v-ons-col>
        <v-ons-card @click="goTo('http://router.vuejs.org/')">vue-router</v-ons-card>
      </v-ons-col>
      <v-ons-col>
        <v-ons-card @click="goTo('http://vuex.vuejs.org/')">vuex</v-ons-card>
      </v-ons-col>
    </v-ons-row>
    <v-ons-row>
      <v-ons-col>
        <v-ons-card @click="goTo('http://vue-loader.vuejs.org/')">vue-loader</v-ons-card>
      </v-ons-col>
      <v-ons-col>
        <v-ons-card @click="goTo('https://github.com/vuejs/awesome-vue')">awesome-vue</v-ons-card>
      </v-ons-col>
    </v-ons-row>
    -->

    <v-ons-fab
      position="bottom right"
      :visible="fabVisible"
    >
      <v-ons-icon icon="fa-plus" style="cursor:pointer;"></v-ons-icon>
    </v-ons-fab>

  </v-ons-page>
</template>

<script>
export default {
  name: "home",
  data() {
    return {
      fabVisible: true,
      msg: "メシガチャ！",
      list: [
        {
          label: "王将"
        },
        {
          label: "カレー"
        },
        {
          label: "ガスト"
        },
        {
          label: "サイゼリア"
        },
        {
          label: "ラーメン"
        },
        {
          label: "honokuni"
        }
      ]
    };
  },
  methods: {
    goTo(url) {
      const newWindow = window.open(url, "_blank");
      newWindow.opener = null;
      newWindow.location = url;
    },
    close() {
      alert("hogeho");
    },
    getFood() {
      const food = document.getElementById("food");
      const random = Math.floor(Math.random() * this.list.length);
      food.innerHTML = this.list[random].label;
    }
  }
};
</script>

<style scoped>
.header {
  margin-top: 30px;
  text-align: center;
}
img {
  max-width: 300px;
}
ons-list-title {
  text-transform: none;
}
ons-list-title:not(:first-of-type) {
  margin-top: 30px;
}
ons-card {
  text-align: center;
}
ons-list-item,
ons-card {
  cursor: pointer;
}
.toolbar-button {
  color: gray;
}
</style>
