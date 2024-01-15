<script>
  // TODO: Uncomment baris kode di bawah untuk meng-import fungsi addNewContact dari services/index.js
  import { addNewContact } from "../services/index";

  // TODO: Uncomment baris kode di bawah untuk mendapatkan fungsi handleGetContacts dari props
  export let handleGetContacts;

  let input = {
    full_name: "",
    phone_number: "",
    email: "",
  };

  function onInputChanged(type, value) {
    switch (type) {
      case "email":
        input.email = value;
        break;
      case "phone_number":
        input.phone_number = value;
        break;
      default:
        input.full_name = value;
        break;
    }
  }

  function resetInputValue() {
    input = {
      full_name: "",
      phone_number: "",
      email: "",
    };
  }

  // TODO: Uncomment baris kode di bawah untuk memanggil fungsi mengirim data kontak baru yang sudah diimport sebelumnya dari services/index.js lalu panggil fungsi untuk mengambil semua data kontak dari api dan mereset value yang ada di setiap input field
  async function handleSubmit() {
    await addNewContact({
      full_name: input.full_name,
      phone_number: input.phone_number,
      email: input.email,
    });

    handleGetContacts();
    resetInputValue();
  }
</script>

<div class="input-contact__form-container">
  <h1 data-cy="header-title">Devcode Contact Manager</h1>
  <div class="input-contact__form">
    <label for="nama">Nama Lengkap</label>
    <div>
      <input
        data-cy="input-nama"
        type="text"
        name="nama"
        bind:value={input.full_name}
        placeholder="Masukkan Nama Lengkap"
        on:change={(e) => onInputChanged("full_name", e.target.value)}
      />
    </div>
    <label for="telepon">No. Telepon</label>
    <div>
      <input
        data-cy="input-telepon"
        type="text"
        name="telepon"
        bind:value={input.phone_number}
        placeholder="Masukkan Nomor Telepon"
        on:change={(e) => onInputChanged("phone_number", e.target.value)}
      />
    </div>
    <label for="email">Email</label>
    <div>
      <input
        data-cy="input-email"
        type="text"
        name="email"
        bind:value={input.email}
        placeholder="Masukkan Email"
        on:change={(e) => onInputChanged("email", e.target.value)}
      />
    </div>
    <button
      data-cy="btn-submit"
      disabled={!input.full_name || !input.phone_number || !input.email}
      on:click={handleSubmit}
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
