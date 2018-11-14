<template>
  <v-ons-page>
    
    <v-ons-toolbar-button @click="$store.commit('splitter/toggle')" style="position: absolute;">
      <v-ons-icon icon="fa-bars" class="side-nav"></v-ons-icon>
    </v-ons-toolbar-button>

    <div class="header">
      <p id="msg">メシガチャ！</p>
      <br>
      <v-ons-card id="food">
        <span>？</span>
      </v-ons-card>
      <br>
      <v-ons-button class="header__button" id="sway-btn" v-if="list.length && !again" modifier="material large" @click="getFood">今日のメシを決める！</v-ons-button>
      <v-ons-button class="header__button" v-if="!list.length" modifier="material large" @click="getFood">
        <v-ons-icon icon="fa-plus" style="margin-right:5px;"></v-ons-icon>からメシを追加してね！
      </v-ons-button>
      <v-ons-button class="header__button" id="sway-btn" v-if="again" modifier="material large" @click="getFood">ん〜もう1回...</v-ons-button>
    </div>

    <v-ons-list-title style="color:white; margin-top:30px;">メシリスト</v-ons-list-title>
    <v-ons-list>
      <v-ons-list-item v-for="item in list" :key="item.link">
        <div class="right" @click="doRemove(item)"><v-ons-icon fixed-width icon="fa-close"></v-ons-icon></div>
        <div class="center">{{ item.label }}</div>
      </v-ons-list-item>
      <v-ons-list-item v-if="!list.length">
        <v-ons-icon icon="fa-plus" style="margin-right:5px;"></v-ons-icon>からメシを追加してね！
      </v-ons-list-item>
    </v-ons-list>

    <v-ons-fab
      position="bottom right"
      :visible="fabVisible" 
      @click="toastVisible = !toastVisible;"
      style="background:#FF9900;"
    >
      <v-ons-icon icon="fa-plus" style="cursor:pointer;"></v-ons-icon>
    </v-ons-fab>

    <v-ons-toast :visible.sync="toastVisible" animation="ascend">
      <input type="text" v-model="newFood" placeholder="新しく追加する？" style="color:white; width:300px; outline:none; background:none; border:none;">
      <button @click="doAdd(); toastVisible = false;">
        <v-ons-icon icon="fa-plus" style="cursor:pointer; color:white;"></v-ons-icon>
      </button>
    </v-ons-toast>

  </v-ons-page>
</template>

<script>
var STORAGE_KEY = "food-list";
var listStorage = {
  fetch: function() {
    var list = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
    list.forEach(function(item, index) {
      item.id = index;
    });
    listStorage.uid = list.length;
    return list;
  },
  save: function(list) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(list));
  }
};

export default {
  name: "home",
  data() {
    return {
      fabVisible: true,
      msg: "メシガチャ！",
      list: [],
      newFood: "",
      toastVisible: false,
      again: false
    };
  },
  watch: {
    list: {
      handler: function(list) {
        listStorage.save(list);
      },
      deep: true
    }
  },
  components: {},
  created() {
    this.list = listStorage.fetch();
  },
  methods: {
    close() {
      alert("hogeho");
    },
    add() {
      alert("tet");
    },
    // 追加処理
    doAdd(event) {
      const label = this.newFood;
      if (!label) {
        return;
      }

      // { ID, label }
      this.list.push({
        id: listStorage.uid++,
        label: this.newFood
      });
      this.newFood = "";
    },
    // 削除処理
    doRemove(item) {
      var index = this.list.indexOf(item);
      this.list.splice(index, 1);
    },
    getFood() {
      $("#food").removeClass("clash");
      const food = document.getElementById("food");
      const msg = document.getElementById("msg");
      const btnMsg = document.getElementById("sway-btn");
      const random = Math.floor(Math.random() * this.list.length);
      const randomFood = this.list[random].label;

      food.innerHTML = "どれにしよかな♪";
      msg.innerHTML = "どれにしよかな♪";
      btnMsg.innerHTML = "どれにしよかな♪";
      $("#food, #msg, #sway-btn").addClass("sway");

      setTimeout(function() {
        food.innerHTML = randomFood;
        msg.innerHTML = "これに決まり！";
        btnMsg.innerHTML = "ん〜もう1回...";

        $("#food").addClass("clash");
        $("#food, #msg, #sway-btn").removeClass("sway");
      }, 2000);
      this.again = true;
    }
  }
};
</script>

<style lang="scss" scoped>
.side-nav {
  margin-top: 10px;
  margin-left: 5px;
  cursor: pointer;
}
.header {
  margin-top: 30px;
  text-align: center;
}
.header__button {
  width: 50%;
  color: black;
  background: #ff9900;
  font-family: "Kosugi maru", sans-serif !important;
}
#msg {
  margin: 0;
  margin-bottom: 10px;
  color: #fff;
  font-family: "Kosugi Maru", sans-serif;
  font-weight: bold;
  font-size: 2.1rem;
}
#food {
  margin: 0 100px;
  margin-bottom: 10px;
  font-family: "Kosugi maru", sans-serif;
}
img {
  max-width: 300px;
}
.list {
  font-family: "Kosugi maru", sans-serif !important;
}
ons-list-title {
  text-transform: none;
}
ons-card {
  text-align: center;
}
ons-list-item,
ons-card {
  cursor: pointer;
}
.toolbar-button {
  color: #fff;
}
::-webkit-input-placeholder {
  color: white;
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
    transform: rotate(-2deg);
  }
  50% {
    transform: rotate(2deg);
  }
  100% {
    transform: rotate(-2deg);
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
