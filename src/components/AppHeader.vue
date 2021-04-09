<template>
  <main class="main"> 
    <h1 class="main-title"> Comics Quiz </h1>
    <h2 class="main-secondary-title"> Score : {{ nbCorrectAnswers }}/{{ numTotal }}</h2>
    <!-- <img src="@/assets/img/background.jpg" alt="" width=200px> -->
  </main>
</template>

<script>
  export default {
    props: [
      'nbCorrectAnswers',
      'numTotal'
    ]
  }
</script>

<style lang="scss" scoped>

.main {
  margin-top: 3rem;
  &-title {
    font-size: 2.2rem;
    font-weight: bold;
    color: black;
  }
  &-secondary-title {
    color: black;
    font-size: 1.4rem;
    background: rgb(131,58,180);
    background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(130,49,66,1) 50%, rgba(252,176,69,1) 100%);
    display: inline-block;
    margin: .8rem 0 2rem 0;
    padding: 1.2rem 1.2rem;
    border-radius: 50%;
    margin-bottom: 2rem;

  }
}

@media only screen and (min-width: 500px) {
  .main-secondary-title {
    margin-bottom: 2rem;
  }

  .main {
    margin-top: 3rem;
    &-title {
      font-size: 3.5rem;
      font-weight: bold;
      color: black;
    }
    &-secondary-title {
      font-weight: bold;
      color: black;
      background: rgb(131,58,180);
      background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(130,49,66,1) 50%, rgba(252,176,69,1) 100%);
      display: inline-block;
      margin: .8rem 0 2rem 0;
      padding: 1.2rem 1.2rem;
      border-radius: 50%;
      box-shadow: rg;
    }
  }
}
</style>