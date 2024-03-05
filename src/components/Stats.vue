<template>
  <div class="card">
    <h2>PageTriage Statistics</h2>
    <p :style="{ fontWeight: 'bold', color: 'gray' }">
      Displaying the statistics of the page triage feed
    </p>
    <div class="statsBody">
      <div class="statcard">
        <span class="countVariable">&nbsp;&nbsp;{{ reviewedarticle }}</span>
        <br />
        Reviewed Articles
      </div>
      <div class="statcard">
        <span class="countVariable">&nbsp;&nbsp;{{ filteredarticle }}</span>
        <br />Filtered Articles
      </div>
      <div class="statcard">
        <span class="countVariable">&nbsp;&nbsp;{{ unreviewedarticle }}</span
        ><br />
        Unreviewed Articles
      </div>
      <div class="statcard">
        <span class="countVariable">&nbsp;&nbsp;{{ unrevieweddraft }}</span>
        <br />Unreviewed Drafts
      </div>
      <div class="statcard">
        <span class="countVariable">&nbsp;&nbsp;{{ unreviewedredirect }}</span
        ><br />
        Unreviewed Redirects
      </div>
    </div>
  </div>
</template>

<script>
import { CdxCard } from "@wikimedia/codex";
import axios from "axios";
export default {
  name: "Stats",
  data() {
    return {
      unreviewedarticle: null,
      unrevieweddraft: null,
      unreviewedredirect: null,
      reviewedarticle: null,
      reviewedredirect: null,
      filteredarticle: null,
    };
  },
  components: {
    CdxCard,
  },
  created() {
    axios
      .get(
        "https://en.wikipedia.org/w/api.php?action=pagetriagestats&format=json&formatversion=2&origin=*",
      )
      .then((resp) => {
        let stats = resp.data.pagetriagestats.stats;
        console.log(stats);
        this.unreviewedarticle = stats.unreviewedarticle.count;
        this.unrevieweddraft = stats.unrevieweddraft.count;
        this.unreviewedredirect = stats.unreviewedredirect.count;
        this.filteredarticle = stats.filteredarticle;
        this.reviewedarticle = stats.reviewedarticle.reviewed_count;
        this.reviewedredirect = stats.reviewedredirect.reviewed_count;
      });
  },
};
</script>

<style scoped>
.card {
  width: 25%;
  border-style: solid;
  border-radius: 2px;
  border-color: white;
  padding: 2rem;
  font-family: Arial, Helvetica, sans-serif;
  background-color: #c5cbe3;
  display: flex;
  flex-direction: column;
  height: 100vh;
  max-height: 100vh;
  text-align: center;
}
.statsBody {
  font-size: 120%;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  height: 100%;
  color: gray;
}
.countVariable {
  font-weight: bold;
  font-size: 140%;
  color: white;
}
.statcard {
  border-style: solid;
  padding-top: 5%;
  padding-bottom: 5%;
  background-color: black;
  line-height: 2;
}
</style>
