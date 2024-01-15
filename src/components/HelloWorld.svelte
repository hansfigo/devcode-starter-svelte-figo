<script>
  // TODO: Uncomment baris kode di bawah ini untuk meng-import gambar logo devcode yang berada di dalam folder lib/assets
  import devcodeLogo from "$lib/assets/devcode-logo.png";
</script>

<div class="hello">
  <!-- TODO: Tambahkan gambar logo devcode yang sudah diimport sebelumnya ke dalam properti src pada elemen img di bawah ini -->
  <img data-cy="devcode-logo" src={devcodeLogo} alt="devcode logo" />
  <div data-cy="devcode-title">
    <!-- TODO: Tambahkan elemen heading 1 di bawah ini dengan berisi kalimat I'm ready for the next challenge! -->
    <h1>I'm ready for the next challenge!</h1>
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
