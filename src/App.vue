<template>
  <v-app>
    <Header :style="[(this.show) ? {filter: 'blur(2px)'} : {filter: 'none'}]" />
    <div class="searchRow row" :style="[(this.show) ? {filter: 'blur(2px)'} : {filter: 'none'}]">
      <v-text-field type="search" class="col-md-2 searchField" append-icon="search"></v-text-field>
    </div>
    <div class="menu row" :style="[(this.show) ? {filter: 'blur(2px)'} : {filter: 'none'}]">
      <span class="headingName">Test</span>
      <div class="forGroup">
        <div class="select">
          <v-select class="selector1" label="Установите автоматическую перезагрузку"></v-select>
          <v-select class="selector2" label="Записей на странице"></v-select>
        </div>
        <span class="pager">Пейджер</span>
        <v-btn-toggle class="btnGroup">
          <v-btn class="icon" flat>
            <v-icon class="iconContent">skip_previous</v-icon>
          </v-btn>
          <v-btn class="icon" flat>
            <v-icon class="iconContent">keyboard_arrow_left</v-icon>
          </v-btn>
          <v-btn class="icon" flat>
            <v-icon class="iconContent">keyboard_arrow_right</v-icon>
          </v-btn>
          <v-btn class="icon" flat>
            <v-icon class="iconContent">skip_next</v-icon>
          </v-btn>
        </v-btn-toggle>
      </div>
    </div>
    <div class="tbl" :style="[(this.show) ? {filter: 'blur(2px)'} : {filter: 'none'}]">
      <v-data-table :headers="headers" sort-icon :items="info" class="table" hide-actions>
        <template v-slot:items="props">
          <td @click="showModal">{{ props.item.Date }}</td>
          <td
            @click="showModal"
            :style="[(props.item.Facility === 'SYSLOG') ? {backgroundColor: '#E9FFDC'} : (props.item.Facility === 'KERN') ? {backgroundColor: '#FFD6D2'} : {backgroundColor: '#FFE2B4'}]"
          >{{ props.item.Facility }}</td>
          <td
            @click="showModal"
            :style="[(props.item.Severity === 'ERR') ? {backgroundColor: '#FFA0A0'} : (props.item.Severity === 'INFO') ? {backgroundColor: '#C4E2FF'} : {backgroundColor: '#B6E198'}]"
          >{{ props.item.Severity }}</td>
          <td @click="showModal">{{ props.item.Host }}</td>
          <td @click="showModal">{{ props.item.Syslogtag }}</td>
          <td @click="showModal">{{ props.item.ProcessID }}</td>
          <td
            @click="showModal"
            :style="[(props.item.Messagetype === 'Syslog') ? {backgroundColor: '#E1FFF5'} : {backgroundColor: 'initial'}]"
          >{{ props.item.Messagetype }}</td>
          <td @click="showModal">{{ props.item.Message }}</td>
        </template>
      </v-data-table>
    </div>
    <v-card class="modalView" v-if="show">
      <v-card-title class="headline">Details for the syslog messages with '442555'</v-card-title>
      <v-card-text class="text">
        <v-list class="column">
          <v-list-tile class="listItem">uID</v-list-tile>
          <v-list-tile class="listItem">Date</v-list-tile>
          <v-list-tile class="listItem">Host</v-list-tile>
          <v-list-tile class="listItem">Messagetype</v-list-tile>
          <v-list-tile class="listItem">Facility</v-list-tile>
          <v-list-tile class="listItem">Severity</v-list-tile>
          <v-list-tile class="listItem">Sysligtag</v-list-tile>
          <v-list-tile class="listItem">Checksum</v-list-tile>
          <v-list-tile class="listItem">Message</v-list-tile>
        </v-list>
        <v-list class="column column2">
          <v-list-tile class="listItem">442554</v-list-tile>
          <v-list-tile class="listItem">2019-07-04 10:06:16</v-list-tile>
          <v-list-tile class="listItem">Host221.92.170.prov.ru</v-list-tile>
          <v-list-tile class="listItem">Syslog</v-list-tile>
          <v-list-tile class="listItem">User</v-list-tile>
          <v-list-tile class="listItem">Notice</v-list-tile>
          <v-list-tile class="listItem">Dhcp, debug, packet</v-list-tile>
          <v-list-tile class="listItem">0</v-list-tile>
          <v-list-tile
            class="listItem"
          >100@213.248.33.249 {cybergrid.exploitbox.ru} SIP/2.0#015#012Via: SIP/2.0/UDP 77.247.110.209:5080;branch=z9</v-list-tile>
        </v-list>
      </v-card-text>
      <i class="material-icons cancelIcon" @click="closeModal">cancel</i>
    </v-card>
  </v-app>
</template>

<script>
import info from "./info.json";

import Header from "./components/Header";
export default {
  name: "App",
  components: {
    Header
  },
  data() {
    return {
      headers: [
        { text: "Date", value: "date", align: "center" },
        { text: "Facility", value: "facility", align: "center" },
        { text: "Severity", value: "severity", align: "center" },
        { text: "Host", value: "host", align: "center" },
        { text: "Sysligtag", value: "syslogtag", align: "center" },
        { text: "ProcessID", value: "processID", align: "center" },
        { text: "MessageType", value: "massType", align: "center" },
        { text: "Message", value: "mess", align: "center" }
      ],
      info: info,
      show: false
    };
  },
  methods: {
    showModal() {
      this.show = true;
    },
    closeModal() {
      this.show = false;
    }
  }
};
</script>

<style>
.searchRow {
  justify-content: center;
  background-color: #eff5fc;
}

.headingName {
  font-size: 26px;
  font-weight: 500;
  color: #4a4a4a;
  line-height: 6;
}

.select {
  display: flex;
  justify-content: flex-end;
}

.menu .theme--light.v-btn-toggle {
  background-color: transparent;
}

.menu {
  min-height: 120px;
  width: 80%;
  justify-content: space-between;
  margin: 0 auto;
}

.forGroup {
  min-width: 600px;
  display: flex;
}

.select {
  padding-top: 6%;
  justify-content: space-between;
  min-width: 530px;
}

.select .v-input__slot:before {
  display: none;
}

.select .v-icon {
  border: 0.5px solid grey;
  border-radius: 15px;
  height: 17px;
  width: 17px;
  font-size: 20px;
}

.selector1 {
  max-width: 290px;
  min-width: 290px;
}

.selector2 {
  max-width: 165px;
  min-width: 165px;
}

.selector1 .v-label,
.selector2 .v-label {
  font-size: 12px;
}

.pager {
  line-height: 12.7;
  font-size: 12px;
  padding-right: 3%;
  padding-left: 3%;
  color: rgba(0, 0, 0, 0.6);
}

.btnGroup {
  max-width: 90px;
  min-width: 90px;
  display: flex;
  justify-content: space-between;
}

.btnGroup .icon {
  padding: 0;
  margin-top: 75%;
}

.btnGroup .v-btn {
  background-color: #0064ff;
  opacity: 1;
  height: 16px;
}

.iconContent {
  font-size: 16px;
  line-height: 0;
}

.icon .v-btn__content {
  color: white;
}

.icon:before {
  display: none;
}

.searchField .v-icon {
  font-size: 21px;
}

.table .v-datatable__progress {
  display: none;
}

.tbl {
  margin: 0 auto;
}

.table .v-datatable thead th.column.sortable,
.table tbody td {
  padding: 0 10px;
  border: 1px solid #d4e5f9;
  vertical-align: inherit;
  color: #4e4e4e;
}

.table tbody td {
  font-weight: 400;
  font-size: 13px;
  width: 150px;
  padding: 0 15px !important;
  color: #a6a6a7;
  text-align: center;
}

.table table.v-table tbody td:nth-child(8) {
  text-align: left;
}

.tablу table.v-table thead th:not(:nth-child(1)) {
  padding: 0;
}

.modalView {
  position: fixed;
  top: 25%;
  max-width: 1000px;
  left: 26%;
  min-height: 565px;
  min-width: 900px;
  background-color: #eff5fc !important;
}

.cancelIcon {
  top: -7%;
  position: absolute;
  left: 100%;
  font-size: 46px;
  color: darkgrey;
}

.cancelIcon:hover {
  cursor: pointer;
}

.headline {
  font-size: 30px !important;
  font-weight: 400;
  margin: 0 auto;
  width: 83%;
  line-height: 42px !important;
  letter-spacing: normal !important;
  font-family: "Roboto", sans-serif !important;
  color: #4e4e4e;
}

.text {
  background-color: #fff;
  display: flex;
  justify-content: space-around;
  padding: 5px;
  min-height: 415px;
}

.text .v-card__text {
  width: 100%;
  margin: 0 auto;
}

.text .v-list {
  line-height: 2;
  position: relative;
  text-align: left;
  font-size: 17px;
  white-space: inherit;
  flex-direction: column;
  display: flex;
}

.text .v-list {
  color: #a6a6a7;
  max-width: 55%;
}

.column2 {
  min-width: 46%;
}

.listItem .v-list__tile {
  min-height: 48px;
}

@media screen and (max-width: 1300px) {
  .modalView {
    top: 5%;
    max-width: 900px;
    left: 15%;
    min-height: 565px;
    min-width: 700px;
  }
  .headline {
    font-size: 24px !important;
    width: 60%;
    line-height: 32px !important;
  }
  .text {
    min-height: 415px;
  }

  .column2 {
    min-width: 58%;
  }
}
</style>

