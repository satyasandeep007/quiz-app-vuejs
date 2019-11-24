 <template>
  <div id="questions">
    <div class="jumbotron">

      <p class="lead"><b>{{currentQuestion.question}}</b></p>
      <hr class="my-4" />
      <p>Answers</p>
      <div>
        <button @click="prev" type="button" class="btn btn-outline-primary">Prev</button>
        <button type="button" class="btn btn-outline-success">Submit</button>
        <button @click="next" type="button" class="btn btn-outline-primary">Next</button>
      </div>
    </div>
  </div>
</template>
 
  <script>
export default {
  props: {
    currentQuestion : Object,
    next : Function,
    prev : Function
  },
  name: "#questions",
  data() {
    return {
      count: 0
    };
  },
  methods: {
    
    method2() {}
  }
};
</script>

<style scoped>
#questions {
  justify-content: center;
  align-content: center;
}
</style> 