<template>
  <div >
    <b-nav>
      <b-nav-item active>Quiz Application</b-nav-item>
      <b-nav-item>Counter: {{ numCorrect }} / {{numTotal }}</b-nav-item>
      <b-nav-item disabled>MehmetEray/github.com</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ]
};
</script>

<style>
</style>