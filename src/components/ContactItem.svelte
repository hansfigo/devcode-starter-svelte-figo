<script>
  import { deleteContact } from "../services/index";

  export let id = 0;
  export let full_name = "";
  export let email = "";
  export let phone_number = "";
  export let handleGetContacts, handleSetSelected;

  // TODO:
  // 1. Buat sebuah fungsi untuk men-dispatch fungsi menghapus kontak yang sudah dibuat sebelumnya di services/index.js dan memanggil fungsi handleGetContacts untuk refresh data kontak
  const handleDeleteContact = async () => {
    await deleteContact(id);

    await handleGetContacts();
  };
  // 2. Buat button edit dengan properti data-cy nya btn-edit, class nya contact-item__button dan contact-item__edit-button serta menjalankan fungsi handleSetSelected ketika di klik
  const handleEditContact = async () => {
    handleSetSelected(id, full_name, email, phone_number);
  };
  // 3. Buat button hapus dengan properti data-cy nya btn-delete, class nya contact-item__button dan contact-item__delete-button serta menjalankan fungsi menghapus kontak yang sudah dibuat sebelumnya ketika di klik
  // 4. Kedua button tersebut dibuat di dalam elemen div dengan class contact-item__button-wrapper
</script>

<div data-cy="item-card" class="contact-item__wrapper">
  <div class="contact-item__first-row">
    <p data-cy="item-name" class="contact-item__name">
      {full_name}
    </p>
    <div class="contact-item__button-wrapper"></div>
  </div>
  <div class="contact-item__second-row">
    <p class="contact-item__phone-email">
      <span data-cy="item-phone">{phone_number}</span> |
      <span data-cy="item-email">{email}</span>
    </p>
  </div>
  <div class="contact-item__button">
    <button data-cy="btn-edit" on:click={() => handleEditContact()}>edit</button
    >
    <button data-cy="btn-delete" on:click={() => handleDeleteContact()}
      >delete</button
    >
  </div>
</div>

<style>
  .contact-item__wrapper {
    margin-bottom: 12px;
    width: 90%;
    height: 48px;
    padding: 24px;
    border-radius: 8px;
    background: #ffffff;
    box-shadow: 0 6px 10px rgb(0 0 0 / 10%);
  }

  .contact-item__first-row {
    display: flex;
    justify-content: space-between;
  }

  .contact-item__second-row {
    text-align: left;
  }

  .contact-item__name {
    margin: 0;
  }

  .contact-item__phone-email {
    margin: 0;
  }

  .contact-item__button-wrapper {
    display: flex;
    gap: 8px;
  }

  .contact-item__button {
    min-width: 64px;
    height: 36px;
    padding-left: 12px;
    padding-right: 12px;
    border: none;
    border-radius: 4px;
    font-size: 14px;
    font-weight: 700;
    color: #ffffff;
    cursor: pointer;
  }

  .contact-item__edit-button {
    background: #16abf8;
  }

  .contact-item__delete-button {
    background: #dc3545;
  }
</style>
