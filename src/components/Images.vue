<template>
  <div class="card">
    <div>
      <h2>Images from Commons</h2>
      <p :style="{ fontWeight: 'bold', color: 'gray' }">
        Some random images fetched from Wikimedia Commons
      </p>
    </div>
    <div class="imagesContainer">
      <span v-for="img in images">
        <img :src="img" class="imageObject" />
      </span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Images",
  data() {
    return {
      images: [],
    };
  },
  created() {
    var apiEndpoint =
      "https://commons.wikimedia.org/w/api.php?action=query&list=allimages&ailimit=12&format=json&origin=*";
    axios.get(apiEndpoint).then((resp) => {
      let allimageObjs = resp.data.query.allimages;
      let imgUrls = [];
      for (let i = 0; i < allimageObjs.length; i++) {
        imgUrls.push(allimageObjs[i]["url"]);
      }
      this.images = imgUrls;
    });
  },
};
</script>

<style scoped>
.card {
  width: 40%;
  border-style: solid;
  border-radius: 2px;
  border-color: white;

  font-family: Arial, Helvetica, sans-serif;
  background-color: #dde0eb;
  height: 100vh;
  text-align: center;
  max-height: 100vh;
  padding: 2rem;
}
.imagesContainer {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
}
.imageObject {
  width: 8rem;
  height: 8rem;
  margin: 1rem;
  border-style: solid;
}
hr {
  border: 2px solid white;
}
</style>
