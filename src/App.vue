<template>
  <div class="container">
    <div :class="!side1 ? 'panelOne' : 'panelOne panelOne_active'">
      <a v-for="(item, index) in list" :key="index" class="link" v-on:click="toggleTwo(item.hijo.item, index)">
        <Icon :name="item.icono" :width="20" :color="'#fff'" />
        <span>{{item.name}}</span>
      </a>
    </div>
    <div :class="!side2 ? 'panelTwo' : 'panelTwo panelTwo_active'">
      <a v-for="(item, index) in list2" :key="index" class="link" v-on:click="toggleTwo(item.hijo.item)">
        <Icon :name="item.icono" :width="20" :color="'#fff'" />
        <span>{{item.name}}</span>
      </a>
    </div>
    <button class="togleButton" v-on:click="toggleOne">Toggle sidebar</button>
  </div>
</template>

<script>
import Icon from './components/icon.vue';
import {menuAdmin} from './sidebar';

export default {
  name: 'App',
  components: {Icon},
  data() {
    return {
      side1: false,
      side2: false,
      list: menuAdmin,
      list2: [],
      idmenu2: 0,
    }
  },
  mounted() {
    console.log(this.list)
  },
  methods: {
    toggleOne: function() {
      if(this.side2) {
        this.side1 = !this.side1;
        this.side2 = !this.side2;
      } else {
        this.side1 = !this.side1;
      }
    },
    toggleTwo: function(e) {
      this.side2 = true;
      this.list2 = e;
    }
  }
}
</script>

<style>
  body {
    padding: 0;
    margin: 0;
    width: 100%;
    height: 100vh;
    background: #fafafa;
    position: relative;
  }
  .container {
    width: 100%;
    height: 100vh;
    background: #fafafa;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .panelOne {
    position: absolute;
    width: 300px;
    height: 100vh;
    background: #212121;
    top: 0;
    left:-300px;
    z-index: 10;
    transition: all ease-in-out .3s;
  }
  .panelOne_active {
    left: 0;
  }

  .panelTwo {
    position: absolute;
    width: 300px;
    height: 100vh;
    z-index: 9;
    background: #bdbdbd;
    top: 0;
    left: -300px;
    transition: all ease-in-out .1s;
  }

  .panelTwo_active {
    left: 300px;
  }

  .togleButton {
    position: absolute;
    top: 20px;
    right: 20px;
    width: 100px;
    height: 40px;
  }

  .link {
    margin-top: 50px;
    font-family: 'Montserrat', sans-serif;
    color: #fff;
    display: flex;
    align-items: center;
    padding: 5px 20px;
    cursor: pointer;
  }
  .link span {
    margin-left: 20px;
  }
</style>
