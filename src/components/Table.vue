<template>
  <div class="card">
    <div>
      <h2>Most watched wiki pages</h2>
      <p :style="{ fontWeight: 'bold', color: 'gray' }">
        Displaying a list of most visited wikipedia pages
      </p>
    </div>
    <br />
    <div>
      <table>
        <tr>
          <th style="width: 20%">Rank</th>
          <th width="50%">Article Name</th>
          <th style="width: 30%">Number of watches</th>
        </tr>
        <tr v-for="(data, idx) in responseData" :key="idx">
          <td>{{ 10 * pageIndex + idx + 1 }}</td>
          <td>{{ data["title"] }}</td>
          <td>{{ data["count"] }}</td>
        </tr>
      </table>
    </div>
    <div>
      <div class="tableControlButtons">
        <cdx-button
          action="progressive"
          size="large"
          class="controlButton"
          @click="pageIndex -= 1"
          :disabled="pageIndex === 0"
          >Previous</cdx-button
        >
        <cdx-button
          action="progressive"
          weight="primary"
          size="large"
          class="controlButton"
          @click="pageIndex += 1"
          >Next</cdx-button
        >
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { CdxButton, CdxCard } from "@wikimedia/codex";
export default {
  name: "Table",
  data() {
    return {
      responseData: [],
      pageIndex: 0,
    };
  },
  components: {
    CdxButton,
    CdxCard,
  },
  watch: {
    pageIndex() {
      axios
        .get(
          "https://en.wikipedia.org/w/api.php?action=query&format=json&list=mostviewed&meta=&formatversion=2&origin=*&pvimoffset=" +
            this.pageIndex * 10,
        )
        .then((resp) => {
          this.responseData = resp.data["query"]["mostviewed"];
        });
    },
  },
  created() {
    axios
      .get(
        "https://en.wikipedia.org/w/api.php?action=query&format=json&list=mostviewed&meta=&formatversion=2&origin=*",
      )
      .then((resp) => {
        this.responseData = resp.data["query"]["mostviewed"];
      });
  },
  computed: {
    mostViewedTable() {
      let strings = [];
      const data = this.responseData;
      console.log(data);
      for (let i = 0; i < data.length; i++) {
        let st = strings.push(st);
      }
      return strings;
    },
  },
};
</script>

<style scoped>
table {
  text-align: center;
  align-items: center;
  width: 100%;
  margin-bottom: 5%;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 100%;
}

table th {
  padding-top: 3%;
  padding-bottom: 3%;
  background-color: black;
  color: white;
  width: max-content;
  font-size: 90%;
}

table td {
  padding-top: 3%;
  padding-bottom: 3%;
  text-overflow: ellipsis;
  text-wrap: nowrap;
}

table tr {
  margin-top: 1px;
  margin-bottom: 1px;
  background-color: rgba(230, 235, 242, 0.96);
}

.tableControlButtons {
  width: 100%;
  display: flex;
  flex-direction: row;
}

.controlButton {
  width: 50%;
}

.card {
  width: 35%;
  border-style: solid;
  border-radius: 2px;
  border-color: white;
  padding: 2rem;
  font-family: Arial, Helvetica, sans-serif;
  background-color: #dde0eb;
  height: 100vh;

  max-height: 100vh;
  text-align: center;
}
</style>
