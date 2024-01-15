<script>
  export let full_name = '';
  export let email = '';
  export let phone_number = '';
</script>

<div data-cy="item-card" class="contact-item__wrapper">
  <div class="contact-item__first-row">
    <p data-cy="item-name" class="contact-item__name">
      {full_name}
    </p>
  </div>
  <div class="contact-item__second-row">
    <p class="contact-item__phone-email">
      <span data-cy="item-phone">{phone_number}</span> | 
      <span data-cy="item-email">{email}</span>
    </p>
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

  /* .contact-item__button-wrapper {
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
    font-weight: bold;
    color: #ffffff;
  }

  .contact-item__edit-button {
    background: #16abf8;
  }

  .contact-item__delete-button {
    background: #dc3545;
  } */
</style>