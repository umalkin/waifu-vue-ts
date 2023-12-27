<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
export default defineComponent({
  name: "Index",
  data() {
    return {
      img: require("../assets/temp.jpg"),
      buttonClicked: false,
    };
  },
  methods: {
    clicked() {
      this.buttonClicked = true;
      this.getWaifu();
    },
    async getWaifu() {
      try {
        await axios
          .get("https://api.waifu.im/search/?is_nsfw=false")
          .then((res) => {
            this.img = res.data.images[0].url;
            this.buttonClicked = false;
          });
      } catch (error) {
        if (error) {
          alert("You have no connection.");
          this.buttonClicked = false;
          this.img = require("../assets/temp.jpg");
        }
      }
    },
  },
});
</script>

<template>
  <div id="main">
    <p>Get A Waifu</p>
    <div v-if="buttonClicked !== true" id="waifu-box" class="box">
      <img id="waifu" :src="img" />
      <div>
        <button @click="clicked()">Get A New Waifu</button>
      </div>
    </div>
    <div v-else="" id="loading-box" class="box">
      <img id="loading" src="../assets/loading.png" />
      <span>Searching for your new waifu...</span>
    </div>
  </div>
</template>

<style scoped>
#main {
  display: flex;
  flex-direction: column;
  align-items: center;
}
p {
  font-size: 5vh;
  font-weight: bold;
  margin-bottom: -3px;
}
/* #waifu-box {
  margin: 10px 320px;
  display: flex;
  flex-direction: column;
  align-items: center;
} */

/* #loading-box {
  height: 63vh;
} */
.box {
  margin: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

#loading {
  width: 30px;
  height: 30px;
  padding: 27vh;
}

span{
  margin-top: -20vh;
}

#waifu {
  height: 60vh;
  width: 30vw;
  /* margin: 10px 320px; */
  margin-bottom: 10px;
  border: 2.5px solid #12d33c;
  border-radius: 2px;
}

button {
  padding: 1.8vh;
  background-color: #54ec75;
  border: 1px solid #12d33c;
  border-radius: 4px;
  cursor: pointer;
  text-align: center;
}
button:active{
  background-color: #12d33c;
}
</style>
