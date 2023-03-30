<template>
  <main>
    <v-card elevation="3" class="box">
      <v-autocomplete label="Ngân hàng" :items="banks" outlined clearable item-value="shortName"
        :item-text="item => item.code + ' - ' + item.shortName" v-model="bank">
      </v-autocomplete>
      <v-text-field v-model="account_number" label="Số tài khoản" outlined clearable></v-text-field>
      <v-text-field v-model="amount" label="Số tiền" outlined clearable></v-text-field>
      <v-text-field v-model="content" label="Nội dung chuyển" outlined clearable></v-text-field>
      <v-btn class="primary mb-10" large block @click="createHandle">Tạo mã</v-btn>
      <div class="justify-center d-flex">
        <img :src="image" alt="">
      </div>
    </v-card>
  </main>
</template>

<script>
import json from '../banks.json'
export default {
  data() {
    return {
      image: "",
      banks: json,
      bank: "MBBank",
      account_number: "",
      content: "",
      amount: ""
    }
  },
  methods: {
    createHandle() {
      if (!this.bank || !this.account_number || !this.content || !this.amount) {
        this.$toast.error("Vui lòng nhập đủ thông tin")
        return
      }
      this.image = `https://img.vietqr.io/image/${this.bank}-${this.account_number}-compact2.jpg?amount=${this.formatAmount(this.amount)}&addInfo=${this.content}&accountName=QR`
    },
    formatAmount(value) {
      return Number(value.replaceAll(",", "")).toFixed(0)
    }
  },
  watch: {
    bank() {
      this.image = ""
    },
    account_number() {
      this.image = ""
    },
    content() {
      this.image = ""
    },
    amount() {
      this.image = ""
    },
  }
};
</script>