<script>
  import { afterUpdate } from "svelte";
  import { addNewContact, updateContactInfo } from "../services/index";

  export let handleGetContacts, handleResetSelected, selectedContact;

  // TODO: Uncomment baris kode di bawah untuk membuat regex yang akan membantu memvalidasi format nomor telepon dan email
  const regexPhoneNumber = /^[0-9]*$/;
  const regexEmail = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;

  // TODO:
  // 1. Buat sebuah fungsi yang akan memvalidasi apakah format dari nomor telepon dan email yang dimasukkan sudah benar atau belum
  // 2. Jika format nomor telepon salah, maka tampilkan sebuah alert dengan isi pesan "Nomor telepon hanya dapat berupa angka."
  // 3. Jika format email salah, maka tampilkan sebuah alert dengan isi pesan "Format email tidak sesuai."
  // 4. Jika format nomor telepon dan email sudah benar, maka lanjutkan proses untuk membuat kontak baru atau meng-update kontak

  let input = {
    full_name: "",
    phone_number: "",
    email: "",
  };
  let selectedId = 0;

  function onSetSelectedContact() {
    if (selectedContact.id !== 0) {
      selectedId = selectedContact.id;
      input.full_name = selectedContact.full_name;
      input.phone_number = selectedContact.phone_number;
      input.email = selectedContact.email;
    }
  }

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
    selectedId = 0;
  }

  async function handleSubmit() {
    if (!regexPhoneNumber.test(input.phone_number)) {
      alert("Nomor telepon hanya dapat berupa angka.");
      return;
    }

    if (!regexEmail.test(input.email)) {
      alert("Format email tidak sesuai.");
      return;
    }

    if (selectedId !== 0) {
      await updateContactInfo({
        id: selectedId,
        data: {
          full_name: input.full_name,
          phone_number: input.phone_number,
          email: input.email,
        },
      });
    } else {
      await addNewContact({
        full_name: input.full_name,
        phone_number: input.phone_number,
        email: input.email,
      });
    }

    handleGetContacts();
    resetInputValue();
    handleResetSelected();
  }

  afterUpdate(() => {
    if (selectedId === 0) {
      onSetSelectedContact();
    }
  });
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
