<template>
  <div id="navbar">
    <div>
      <nav class="nav justify-content-center">
        <b-nav-item disabled><b><h1>Quiz App
              <span class="badge badge-secondary">Counter:  {{ numCorrect }}/{{ numTotal }}</span></h1></b>
        </b-nav-item>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'numCorrect',
    'numTotal'
  ]
}

</script>

<style scoped></style>
