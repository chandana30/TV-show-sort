<template>
  <h1>Episodes Name Listing in Alphabetical Order</h1>
  <br />
  
  <div v-for="(seasonData, group, index) in groupbySeason" :key="index">
    <h3>Episode names Starts with :{{ group }}</h3>
    <hr />
    <EpisodeDesc :episodeLists="seasonData" >
    <template v-slot:btn1>
      <button>Button 1</button>
    </template>
    <template v-slot:btn2>
      <button>Button 2</button>
    </template>
    </EpisodeDesc>
  </div>
  
</template>

<script>
import { defineAsyncComponent } from "vue";
const EpisodeDesc = defineAsyncComponent({
  loader: () =>
    import('./EpisodeDesc.vue'/*webpackChunkName: "Episode Name"*/),
  delay: 500
});
import data from "@/data.json";
export default {
  components: {
    EpisodeDesc
  },
  name: "home",
  data() {
    return {
      episodeLists: [],
    };
  },
  computed: {
    groupbySeason() {
      let list = {};
      let alpha = [];
      for (let i = 65; i <= 90; i++) {
        alpha.push(String.fromCharCode(i))
      }
      this.episodeLists.forEach((ele) => {
        var x = ele.name.charAt(4);
        for (let j = 0; j < 26; j++) {
          if (alpha[j] === x) {
            if (Object.keys(list).includes(x)) {
              list[x] = [...list[x], ele];
            } else {
              list[x] = [ele];
            }
          }
        }
      });
      console.log({ list });
      list = Object.entries(list).sort((a, b) => {
        if (b > a) {
          return -1;
        } else if (b < a) {
          return 1;
        } else return 0;
      });
      list = Object.fromEntries(list);
      console.log();
      return list;
    },
  },
  created() {
    this.episodeLists = data && data._embedded && data._embedded.episodes;
    console.log(this.episodeLists);
  },
  methods: {},
};
</script>

<style scoped>
h1{
  text-align:center;
  color:black;
  font-style: italic;
  text-decoration: underline;
  text-decoration-color: gold;
}
h3{
  color: blue;
  text-shadow:1.2px 1.2px gray;


}
hr {
  border: 3px solid goldenrod;
  border-radius: 3px;
}
</style>