<div class="input-contact__form-container">
  <h1 data-cy="header-title">Devcode Contact Manager</h1>
  <div class="input-contact__form">
    <label for="nama">Nama Lengkap</label>
    <div>
      <input
        data-cy="input-nama"
        type="text"
        name="nama"
        placeholder="Masukkan Nama Lengkap"
      />
    </div>
    <label for="telepon">No. Telepon</label>
    <div>
      <input
        data-cy="input-telepon"
        type="text"
        name="telepon"
        placeholder="Masukkan Nomor Telepon"
      />
    </div>
    <label for="email">Email</label>
    <div>
      <input
        data-cy="input-email"
        type="text"
        name="email"
        placeholder="Masukkan Email"
      />
    </div>
    <button
      data-cy="btn-submit"
    >
      Simpan
    </button>
  </div>
</div>

<style>
  .input-contact__form {
    padding-left: 15%;
    padding-right: 15%;
    text-align: left;
  }

  h1 {
    text-align: center;
  }

  label {
    font-size: 14px;
    font-weight: bold;
  }

  input {
    margin-top: 4px;
    margin-bottom: 16px;
    width: 98%;
    height: 28px;
  }

  button {
    width: 100%;
    height: 36px;
    border: none;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    background: #198754;
    color: #ffffff;
  }

  button:disabled {
    opacity: 0.5;
  }
</style>