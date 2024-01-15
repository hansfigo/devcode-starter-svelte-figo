<script>
  // TODO: Uncomment baris kode di bawah untuk meng-import onMount component lifecycle hooks dari svelte
  import { onMount } from "svelte";

  // TODO: Uncomment baris kode di bawah untuk meng-import fungsi mengambil data dari API dari folder services
  import { getAllContactsData } from "../../services/index";

  import InputContactForm from "../../components/InputContactForm.svelte";

  // TODO: Uncomment baris kode di bawah untuk meng-import komponen ContactItem
  import ContactItem from "../../components/ContactItem.svelte";

  // TODO: Uncomment baris kode di bawah untuk membuat variabel yang akan menyimpan data list kontak dari API
  let contactsList = [];

  // TODO: Uncomment baris kode dibawah untuk mengeksekusi onMount hooks yang di dalamnya berisi pemanggilan fungsi mengambil data kontak dari API dan memasukkan datanya ke dalam variabel contactsList
  onMount(async () => {
    const res = await getAllContactsData();
    contactsList = res?.data?.data;
  });
</script>

<div>
  <div class="home">
    <div class="container">
      <InputContactForm />
      <div class="contact-list__container">
        <!-- TODO: Uncomment baris kode di bawah ini untuk menampilkan komponen ContactItem yang berisi data kontak sesuai dengan jumlah data kontak yang didapat dari API -->
        {#each contactsList as contact}
          <ContactItem
            full_name={contact.full_name}
            email={contact.email}
            phone_number={contact.phone_number}
          />
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
