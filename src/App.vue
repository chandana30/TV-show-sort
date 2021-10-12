 <template>
  <div class="main">
    <Suspense>
      <template #default>
        <Home />
      </template>
      <template #fallback>
        <Shows/>
      </template>
    </Suspense>
  </div>
</template>

<script>
import Home from './components/home/Home.vue';
import Shows from "./components/home/Shows.vue";
export default {
  name: "App",
  data() {
    return {
      checkedData: [],
    };
  },
  components:{
    Home,
    Shows
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: blue;
  margin-top: 60px;
}
</style>
