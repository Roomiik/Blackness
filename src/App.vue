<script>
import { RouterLink, RouterView } from 'vue-router'
import Base from "./Base.json";
import IsBlacknes from "./IsBlackness.json";

export default {
  data() {
    return {
      Users: Base,
      selectedDate: null,
      datepickerFormat: "dd.MM.yyyy",
      IsBlackness: IsBlacknes,
      dates: null,
      checked: null,
    }
  },
  methods: {
    GetDate() {
      let dat = new Date();
      return `${dat.getDate()}.${dat.getMonth()}.${dat.getFullYear()} - ${dat.getHours()}:${dat.getMinutes()}:${dat.getMilliseconds()}`
    },
    selectDate(date) {
      console.log(date);
    },
  },
}
</script>

<template>
  <nav class="navbar cont navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <RouterLink class="nav-link" to="/">Home</RouterLink>
      </li>
        <li class="nav-item"><RouterLink class="nav-link" to="/register">Register</RouterLink>
      </li>
      <li class="nav-item">
        <RouterLink class="nav-link" href="#" to="/login">Login</RouterLink>
      </li>
    </ul>
  </div>
</nav>
<div>

    <div>
      <h3>Виберіть дату:</h3>
      <input type="date" v-model="dates" v-on:input="selectDate(dates)">
    </div>

    <div v-if="selectedDate">
      <h3>Список для обраної дати:</h3>
      <ul>
        <li v-for="item in filteredData" :key="item.id">{{ item.first }} {{ item.name }} {{ item.blackness }}</li>
      </ul>
    </div>
    <input type="checkbox" id="checkbox" v-model="checked" />
    <label for="checkbox">Всі чергували</label>
  </div>

  <div class="cont">
    <div class="menu">
      <div class="name">
        <span class="first">Прізвище</span>
        <span class="names">Імя</span>
        <span class="nameb">По батькові</span>
        <span class="blackness">Чергував</span>
        <span class="date">Дата</span>
      </div>
    </div>

    <div class="menu" v-if="dates === null">
      <div class="name" v-for="(item, i) in Users" :key="i">
        <span class="first">{{ item.first }}</span>
        <span class="names">{{item.name}}</span>
        <span class="nameb">{{item.bname}}</span>
        <span class="blackness">{{item.blackness}}</span>
        <span class="date">{{GetDate()}}</span>
      </div>
    </div>

    <div class="menu" v-else>
        <div v-for="(item, i) in IsBlackness" :key="i"> 
          <div v-if="i == dates || checked == true">
      <div class="name" v-for="items in item" :key="items.id">
          <span class="first">{{ Users.filter((key) => key.id == items.id)[0].first }}</span>
          <span class="names">{{Users.filter((key) => key.id == items.id)[0].name}}</span>
          <span class="nameb">{{Users.filter((key) => key.id == items.id)[0].bname}}</span>
          <span class="blackness">{{Users.filter((key) => key.id == items.id)[0].blackness}}</span>
          <span class="date">{{i}}</span>
        </div></div>
      </div>
    </div>
  </div>
  <RouterView />
</template>

<style scoped>
.names, .first, .nameb, .blackness, .date {
  margin: 20px;
}
.navbar {
  float: right;
}

.name {
  display: flex;
  justify-content: space-around;
  gap: 1px;
  margin: 20px 0;
}
.menu {
  padding: 5% 0 10px 10px;
}

.name {
  width: 207vh;
  background: #DDD;
  align-content: center;
  border-radius: 4px;
}
</style>
