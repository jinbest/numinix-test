<template>
  <div class="customer">
    <div class="customer-container">
      <img
        :src="customer.img_src || require('../assets/img/customers/bret.png')"
        alt="customer-avatar"
        class="avatar-desktop"
      />
      <div class="customer-info-1">
        <div class="customer-names">
          <h1>{{ customer.name }}</h1>
          <p>{{ `@${customer.username}` }}</p>
          <p class="company-name">
            {{ `"${customer.company.catchPhrase}"` }}
          </p>
        </div>
        <div class="avatar-mobile">
          <img
            :src="
              customer.img_src || require('../assets/img/customers/bret.png')
            "
            alt="customer-avatar"
          />
        </div>
      </div>
      <div class="customer-info-2">
        <div>
          <img src="../assets/img/icons/mail.svg" alt="mail" />
          <p>{{ customer.email }}</p>
        </div>
        <div>
          <img src="../assets/img/icons/address.png" alt="address" />
          <p>{{ formatAddress(customer.address) }}</p>
        </div>
        <div>
          <img src="../assets/img/icons/phone.svg" alt="phone" />
          <p>{{ customer.phone }}</p>
        </div>
        <div>
          <img src="../assets/img/icons/website.svg" alt="website" />
          <p>{{ customer.website }}</p>
        </div>
        <div>
          <img src="../assets/img/icons/company-name.svg" alt="company-name" />
          <p>{{ customer.company.name }}</p>
        </div>
        <div>
          <img src="../assets/img/icons/industrial.svg" alt="industrial" />
          <p>{{ customer.company.bs }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CustomerComp",
  props: {
    customer: Object,
  },
  methods: {
    formatAddress(address) {
      return `${address.street}, ${address.suite}, ${address.city}, ${address.zipcode}, ${address.geo.lat}, ${address.geo.lng}`;
    },
  },
};
</script>

<style scoped>
.customer {
  padding: 20px;
  box-sizing: border-box;
  width: 25%;
}
.customer-container {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  background: white;
  display: flex;
  flex-direction: column;
  text-align: left;
  border-radius: 8px;
  overflow: hidden;
}
.customer-info-1 {
  padding: 20px 20px 0;
  display: flex;
  width: 100%;
  box-sizing: border-box;
}
.customer-names h1 {
  font-size: 20px;
  color: #202223;
}
.customer-names > p {
  font-size: 14px;
  color: #919191;
}
.company-name {
  color: #52c5ff !important;
  line-height: 20px;
  padding: 10px 0;
}
.customer-info-2 {
  padding: 0 20px 20px;
  width: 100%;
  box-sizing: border-box;
}
.customer-info-2 div {
  width: 100%;
  display: flex;
  padding: 3px 0;
}
.customer-info-2 div img {
  width: 16px;
  max-height: 16px;
  margin-right: 10px;
}
.customer-info-2 div p {
  font-size: 14px;
  color: #202223;
}
.avatar-desktop {
  width: 100%;
}
.avatar-mobile {
  display: none;
  text-align: center;
}
.avatar-mobile img {
  height: 100%;
  max-width: 100%;
}
@media (max-width: 1300px) {
  .customer {
    width: 33.33%;
  }
}
@media (max-width: 960px) {
  .customer {
    padding: 10px;
  }
}
@media (max-width: 768px) {
  .customer {
    width: 50%;
    padding: 20px;
  }
}
@media (max-width: 600px) {
  .avatar-desktop {
    display: none;
  }
  .avatar-mobile {
    display: flex;
    width: 120px;
    height: 120px;
    border-radius: 8px;
    overflow: hidden;
    justify-content: center;
    align-items: center;
    margin-left: auto;
    box-sizing: border-box;
  }
  .customer {
    width: 100%;
    padding: 0px;
    margin-bottom: 20px;
  }
  .customer-names {
    width: calc(100% - 130px);
    box-sizing: border-box;
  }
}
@media (max-width: 425px) {
  .customer-info-1 {
    padding: 12px;
  }
  .avatar-mobile {
    width: 80px;
    height: 80px;
  }
  .customer-names {
    width: calc(100% - 90px);
  }
}
</style>
