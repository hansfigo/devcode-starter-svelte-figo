<script>
  import { onMount } from 'svelte';
  import { getAllContactsData } from '../../services/index';

  import InputContactForm from '../../components/InputContactForm.svelte';
  import ContactItem from '../../components/ContactItem.svelte';

  let contactsList = []
  let selectedContact = {
    id: 0,
    full_name: '',
    phone_number: '',
    email: '',
  }

  function handleSetSelectedContact(id, full_name, phone_number, email) {
    selectedContact = { id, full_name, phone_number, email }
  }

  function handleResetSelectedContact() {
    selectedContact = {
      id: 0,
      full_name: '',
      phone_number: '',
      email: '',
    }
  }

  async function handleGetContactsData() {
    const res = await getAllContactsData();
    contactsList = res?.data?.data;
  }

  onMount(() => {
    handleGetContactsData();
  })
</script>

<div>
  <div class="home">
    <div class="container">
      <InputContactForm handleGetContacts={handleGetContactsData} handleResetSelected={handleResetSelectedContact} selectedContact={selectedContact} />
      <div class="contact-list__container">
        {#each contactsList as contact}
          <ContactItem id={contact.id} full_name={contact.full_name} email={contact.email} phone_number={contact.phone_number} handleGetContacts={handleGetContactsData} handleSetSelected={handleSetSelectedContact} />
        {/each}
      </div>
    </div>
  </div>
</div>

<style>
  .home {
    display: flex;
    justify-content: center;
  }

  .container {
    margin-top: 8px;
    padding: 18px;
    width: 50%;
    height: 100%;
    border: solid 4px #d4d4d4;
    background: #f4f4f4;
  }

  .contact-list__container {
    margin-top: 48px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>