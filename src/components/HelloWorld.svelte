<script>
  import devcodeLogo from '$lib/assets/devcode-logo.png'
</script>

<div class="hello">
  <img data-cy="devcode-logo" src={devcodeLogo} alt="devcode logo" />
  <div data-cy="devcode-title">
    <h1>I'm ready for the next challenge!</h1>
  </div>
  <div data-cy="router-button">
    <a href="/contacts" class="router__btn">
      Level Selanjutnya
    </a>
  </div>
</div>

<style>
  .hello {
    margin: 15% 0 0;
    text-align: center;
  }

  img {
    width: 15%;
    height: 15%;
  }
</style>