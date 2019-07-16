<template>
  <div class="header row">
    <div class="title">
      <span class="titleName">FlyData Collector</span>
    </div>
    <div class="common">
      <v-toolbar-items class="nav">
        <v-btn flat>Статистика</v-btn>
        <v-btn flat>Админ. центр</v-btn>
        <v-btn class="logBtn" flat>Выйти</v-btn>
        <v-btn flat>Войти как админ.</v-btn>
      </v-toolbar-items>
      <v-text-field class="search" label="Поиск..."></v-text-field>
    </div>
    <!-- <div class="col-md-1"></div> -->
  </div>
</template>

<script>
export default {};
</script>

<style>
.header {
  width: 80%;
  margin: 0 auto;
  min-height: 70px;
  justify-content: space-between;
}

.common {
  display: flex;
  min-width: 635px;
  justify-content: space-between;
}

.title {
  text-align: right;
}

.titleName {
  line-height: 3;
  font-size: 28px;
  color: #4A4A4A;
}

.nav {
  justify-content: flex-end;
}

.nav .v-btn {
  text-transform: capitalize;
  padding: 10px;
}

.nav .v-btn__content {
  height: 30px;
  padding: 5px;
  font-size: 13px;
  font-weight: 300;
}

.nav .v-btn__content:hover {
  background-color: rgba(0, 0, 0, 0.1)
}

.logBtn .v-btn__content {
  background-color: #0064ff;
  color: white;
}

.nav .v-btn:before {
  display: none;
}

.search {
  max-width: 150px;
  padding-top: 18px;
}

.search .v-label {
  line-height: 30px;
  font-size: 14px;
}

.search .v-input__slot {
  margin-bottom: 0;
}

.search .v-input__slot:before {
  display: none;
}

</style>


