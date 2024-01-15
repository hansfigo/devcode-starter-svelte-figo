<script>
  import { afterUpdate } from "svelte";
  import { addNewContact, editContact } from "../services/index";

  export let handleGetContacts, handleResetSelected, selectedContact;

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

  // TODO:
  // 1. Buat metode untuk dispatch fungsi ubah data kontak yang sudah dibuat sebelumnya di service/index.js di dalam fungsi handleSubmit
  // 2. Pada fungsi handleSubmit, buat percabangan dengan kondisi ketika nilai dari id lebih dari 0, maka jalankan fungsi ubah data kontak dan untuk sebaliknya, maka jalankan fungsi untuk tambah kontak baru

  async function handleSubmit() {
    const payload = {
      full_name: input.full_name,
      phone_number: input.phone_number,
      email: input.email,
    };
    if (selectedId > 0) {
      console.log("Edit");
      await editContact(selectedId, payload);

      handleGetContacts();
    } else {
      console.log("New");
      await addNewContact(payload);

      handleGetContacts();
      resetInputValue();
      handleResetSelected();
    }
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
