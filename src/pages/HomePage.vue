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
      <p>今日のメシは...</p>
      <v-ons-card id="food" style="margin: 10px 50px;">
        <span>？</span>
      </v-ons-card>
      <v-ons-button modifier="material large" @click="getFood" style="width:70%; color:black; background:#ffeb3b;">今日のメシを決める！</v-ons-button>
    </div>

    <v-ons-list-title style="margin-top:30px;">メシリスト</v-ons-list-title>
    <v-ons-list>
      <v-ons-list-item v-for="item in list" :key="item.link">
        <div class="right" @click="close"><v-ons-icon fixed-width icon="fa-close"></v-ons-icon></div>
        <div class="center">{{ item.label }}</div>
      </v-ons-list-item>
    </v-ons-list>

    <v-ons-fab
      position="bottom right"
      :visible="fabVisible" 
      @click="toastVisible = !toastVisible"
    >
      <v-ons-icon icon="fa-plus" style="cursor:pointer;"></v-ons-icon>
    </v-ons-fab>

    <v-ons-toast :visible.sync="toastVisible" animation="ascend">
      FABs up!
      <button @click="toastVisible = false">ok</button>
    </v-ons-toast>

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
          label: "hoge"
        }
      ],
      toastVisible: false
    };
  },
  components: {},
  mounted() {},
  methods: {
    close() {
      alert("hogeho");
    },
    doAdd(value) {
      this.list.push({
        id: todoStorage.uid++,
        label: label.value
      });
      label.value = "";
    },
    doRemove(item) {
      var index = this.list.indexOf(item);
      this.list.splice(index, 1);
    },
    getFood() {
      $("#food").removeClass("clash");
      const food = document.getElementById("food");
      const random = Math.floor(Math.random() * this.list.length);
      const randomFood = this.list[random].label;

      food.innerHTML = "どれにしよかな♪";
      $("#food").addClass("sway");

      setTimeout(function() {
        food.innerHTML = randomFood;
        $("#food").addClass("clash");
        $("#food").removeClass("sway");
      }, 2000);
    }
  }
};
</script>

<style lang="scss" scoped>
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

/************************
******* animation *******
************************/
.sway {
  display: inline-block;
  animation: sway 1s infinite;
}
@keyframes sway {
  0% {
    transform: rotate(-3deg);
  }
  50% {
    transform: rotate(3deg);
  }
  100% {
    transform: rotate(-3deg);
  }
}
.clash {
  animation: clash 1s infinite;
}
@keyframes clash {
  0% {
    transform: scale(1, 1) translate(0%, 0%);
  }
  40% {
    transform: scale(0.95, 1.2) translate(0%, -10%);
  }
  50% {
    transform: scale(1.1, 0.9) translate(0%, 5%);
  }
  60% {
    transform: scale(0.95, 1.05) translate(0%, -3%);
  }
  70% {
    transform: scale(1.05, 0.95) translate(0%, 3%);
  }
  80% {
    transform: scale(1, 1) translate(0%, 0%);
  }
  100% {
    transform: scale(1, 1) translate(0%, 0%);
  }
}
</style>
