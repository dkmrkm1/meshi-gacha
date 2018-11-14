<template>
  <v-ons-page>
    <v-ons-toolbar modifier="transparent" style="background:#146eb4;"></v-ons-toolbar>
    <div class="header">
      <img src="../assets/logo.png" alt="meshi-logo">
    </div>

    <v-ons-list-title style="margin-right:10px; text-align:right; color:white">@duuun02</v-ons-list-title>
    <!--
    <v-ons-list>
      <router-link to="/about">
        <v-ons-list-item modifier="chevron">
          <div>hogehoge</div>
        </v-ons-list-item>
      </router-link>

      <v-ons-list-item modifier="chevron" v-for="item in essentialLinks" v-link="item.link" :key="item.link">
        <div class="left"><v-ons-icon fixed-width :icon="item.icon"></v-ons-icon></div>
        <div class="center">{{ item.label }}</div>
      </v-ons-list-item>
    </v-ons-list>
    -->
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
</style>
