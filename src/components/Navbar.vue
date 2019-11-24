<template>
  <div id="navbar">
    <div>
      <nav class="nav justify-content-center">
        <b-nav-item disabled>
          <b>
            <h2>
              Quiz App
              <span class="badge badge-secondary">Counter: {{ numCorrect }}/{{ numTotal }}</span>
            </h2>
          </b>
        </b-nav-item>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  props: ["numCorrect", "numTotal"]
};
</script>

<style scoped>
.nav {
  background-color: rgb(4, 243, 4);
  color: white;
}
h2 {
  color: white;
  font-weight: bolder;
}
</style>
