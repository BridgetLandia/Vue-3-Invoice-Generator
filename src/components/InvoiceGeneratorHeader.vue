<script setup lang="ts">
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'

defineProps<{
  invoiceHeader: {
    businessName: string
    from_taxNumber: string
    from_address1: string
    from_address2: string
    from_city: string
    from_postcode: string
    clientName: string
    client_taxNumber: string
    client_address1: string
    client_address2: string
    client_city: string
    client_postcode: string
    invoice_id: string
    invoice_date: string
    purchase_order: string
    invoice_due: string
  }
}>()
</script>

<template>
  <fieldset>
    <legend><h2 classname="">Header</h2></legend>
    <v-row justify="center">
      <v-col md="4">
        <h3>From</h3>
        <v-text-field
          label="Business Name"
          type="text"
          v-model.trim="invoiceHeader.businessName"
          placeholder="Business Name"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Tax Number"
          v-model.trim="invoiceHeader.from_taxNumber"
          placeholder="Tax Number"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Address Line 1"
          v-model.trim="invoiceHeader.from_address1"
          placeholder="Address Line 1"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Address Line 2"
          v-model.trim="invoiceHeader.from_address2"
          placeholder="Address Line 2"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Solo"
          v-model.trim="invoiceHeader.from_city"
          placeholder="City"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Postcode"
          v-model.trim="invoiceHeader.from_postcode"
          placeholder="Postcode"
          variant="solo"
        ></v-text-field>
      </v-col>
      <v-col md="4">
        <h3>To</h3>
        <v-text-field
          type="text"
          label="Business Name"
          v-model.trim="invoiceHeader.clientName"
          placeholder="Business Name"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Tax Number"
          v-model.trim="invoiceHeader.client_taxNumber"
          placeholder="Tax Number"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Address Line 1"
          v-model.trim="invoiceHeader.client_address1"
          placeholder="Address Line 1"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Address Line 2"
          v-model.trim="invoiceHeader.client_address2"
          placeholder="Address Line 2"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="City"
          v-model.trim="invoiceHeader.client_city"
          placeholder="City"
          variant="solo"
        ></v-text-field>
        <v-text-field
          type="text"
          label="Postcode"
          v-model.trim="invoiceHeader.client_postcode"
          placeholder="Postcode"
          variant="solo"
        ></v-text-field>
      </v-col>
      <v-col md="4">
        <h3>Details</h3>
        <v-text-field
          label="Invoice Number"
          v-model.trim="invoiceHeader.invoice_id"
          placeholder="Invoice Number"
          variant="solo"
        ></v-text-field>
        <v-text-field
          label="Purchase Order Number"
          v-model.trim="invoiceHeader.purchase_order"
          placeholder="PO Number"
          variant="solo"
        ></v-text-field>
        <label for="Issue Date">Issue Date</label>
        <VueDatePicker
          :enable-time-picker="false"
          model-type="dd.MM.yyyy"
          v-model="invoiceHeader.invoice_date"
        ></VueDatePicker>
        <label for="Due Date">Due Date</label>
        <VueDatePicker
          :enable-time-picker="false"
          model-type="dd.MM.yyyy"
          v-model="invoiceHeader.invoice_due"
        ></VueDatePicker>
      </v-col>
    </v-row>
  </fieldset>
</template>

<style>
#main_title {
  padding: 1rem;
}
#invoice_title {
  font-size: 2rem;
  padding-left: 2rem;
}
#subtitle {
  margin-left: 2rem;
}
.button-remove {
  font-weight: 900;
  font-size: 2rem;
}
#invoice_notes {
  border: 1px solid grey;
}
#title_container {
  display: flex;
  align-items: center;
}
#logo {
  height: 50px;
  position: relative;
  margin-left: -4rem;
  margin-top: 3.5rem;
}
.labels {
  font-weight: 700;
}
.item-index {
  padding-bottom: 22px;
}
.item-button {
  margin-bottom: 22px;
  margin-left: 5px;
  padding: 6rem;
}
tr:nth-child(2) {
  background: #f5eee8;
}
.border_bottom {
  border-bottom: lightgrey solid 2px;
}

td {
  padding-top: 26px;
}
#small-table {
  width: 100%;
}
#small-table td:nth-child(2) {
  width: 80%;
}
#small-table td {
  width: 20%;
}
#small-table td:nth-child(2) {
  width: 80%;
}
.pdf-icon {
  margin-right: 1rem;
}

button,
input,
select,
textarea {
  background-color: transparent;
  border-style: border solid 1px;
}
.datepicker input {
  border-bottom: grey 2px solid;
}
</style>
