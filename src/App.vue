 <template>
  <div id="app">
    <Navbar />
    <b-container class="bv-example-row">
      <b-row>
      <b-col sm="8" offset="2">
        <Questions 
        v-bind:currentQuestion="questions[index]"
        v-bind:next="next"
        v-bind:prev="prev" />
      </b-col>
      </b-row>
    </b-container>
  </div>
</template>
 
  <script>
import Questions from "./components/Questions";
import Navbar from "./components/Navbar";
export default {
  name: "#app",
  components: {
    Navbar,
    Questions
  },
  data() {
    return {
      questions : [],
      index : 0
    };
  },
  mounted () {
    fetch('https://opentdb.com/api.php?amount=10&category=21&difficulty=easy&type=multiple',{
      method:'get'})
      .then((response)=>{
        return response.json()
      })
      .then((jsonData)=>{
        this.questions=jsonData.results
      })
  },
  methods: {
    next() {
      this.index++
    },
     prev() {
      this.index--
    },
  },
};
</script>
 
 <style scoped>
</style> 