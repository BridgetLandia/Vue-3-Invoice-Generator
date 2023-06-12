<script setup lang="ts">
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
  invoiceItems: Array<{
    description: string
    qty: string
    price: string
    discount: string
    tax: string
    discount_amount: string
    tax_amount: string
    total: string
  }>

  calculateTotal: number
  itemsDiscountTotal: number
  itemsTaxTotal: number

  invoiceItemTotal: (index) => void

  bankDetails: {
    bank_name: string
    bank_account: string
    swift_code: string
  }
  invoiceNotes: string
}>()
</script>

<template>
  <v-card class="ma-12 pa-16">
    <div id="invoice_template">
      <v-row justify="center">
        <v-col md="4">
          <h3>From</h3>
          <label class="labels" for="Businesss Name">Business Name</label>
          <div>{{ invoiceHeader.businessName }}</div>
          <label class="labels" for="Tax Number">Tax Number</label>
          <div>{{ invoiceHeader.from_taxNumber }}</div>
          <label class="labels" for="Address Line 1">Address Line 1</label>
          <div>{{ invoiceHeader.from_address1 }}</div>
          <label class="labels" for="Address Line 2">Address Line 2</label>
          <div>{{ invoiceHeader.from_address2 }}</div>
          <label class="labels" for="City">City</label>
          <div>{{ invoiceHeader.from_city }}</div>
          <label class="labels" for="Postcode">PostCode</label>
          <div>{{ invoiceHeader.from_postcode }}</div>
        </v-col>
        <v-col md="4">
          <h3>To</h3>
          <label class="labels" for="Businesss Name">Business Name</label>
          <div>{{ invoiceHeader.clientName }}</div>
          <label class="labels" for="Tax Number">Tax Number</label>
          <div>{{ invoiceHeader.client_taxNumber }}</div>
          <label class="labels" for="Address Line 1">Address Line 1</label>
          <div>{{ invoiceHeader.client_address1 }}</div>
          <label class="labels" for="Address Line 2">Address Line 2</label>
          <div>{{ invoiceHeader.client_address2 }}</div>
          <label class="labels" for="City">City</label>
          <div>{{ invoiceHeader.client_city }}</div>
          <label class="labels" for="Postcode">PostCode</label>
          <div>{{ invoiceHeader.client_postcode }}</div>
        </v-col>
        <v-col md="4">
          <h3>Details</h3>
          <label class="labels" for="Invoice Number">Invoice Number</label>
          <div>{{ invoiceHeader.invoice_id }}</div>
          <label class="labels" for="Issue Date">Purchase Order</label>
          <div>{{ invoiceHeader.purchase_order }}</div>
          <label class="labels" for="Issue Date">Issue Date</label>
          <div>{{ invoiceHeader.invoice_date }}</div>
          <label class="labels" for="Issue Date">Due Date</label>
          <div>{{ invoiceHeader.invoice_due }}</div>
        </v-col>
      </v-row>
      <v-row>
        <v-col md="12">
          <h3>Items:</h3>
          <v-table>
            <thead>
              <tr>
                <th class="text-left">No.</th>
                <th class="text-left">Desciption</th>
                <th class="text-left">Qty</th>
                <th class="text-left">Price</th>
                <th class="text-left">Discount</th>
                <th class="text-left">Discount Amount</th>
                <th class="text-left">Tax</th>
                <th class="text-left">Tax Amount</th>
                <th class="text-left">Total</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in invoiceItems" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ item.description }}</td>
                <td>{{ item.qty }}</td>
                <td>{{ item.price }}</td>
                <td>{{ item.discount }}</td>
                <td>{{ item.discount_amount }}</td>
                <td>{{ item.tax }}</td>
                <td>{{ item.tax_amount }}</td>
                <td>{{ item.total }}</td>
              </tr>
              <tr>
                <td>Discount:</td>
                <td>{{ itemsDiscountTotal }}</td>
              </tr>
              <tr>
                <td>Tax:</td>
                <td>{{ itemsTaxTotal }}</td>
              </tr>
              <tr>
                <td>Total:</td>
                <td>{{ calculateTotal }}</td>
              </tr>
            </tbody>
          </v-table>
        </v-col>
      </v-row>
      <v-row>
        <v-col md="4">
          <h3>Bank Information:</h3>
          <label for="Invoice Number">Bank Name</label>
          <div>{{ bankDetails.bank_name }}</div>
          <label for="Issue Date">Account number</label>
          <div>{{ bankDetails.bank_account }}</div>
          <label for="Due Date">SWIFT Code</label>
          <div>{{ bankDetails.swift_code }}</div>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <label for="Invoice Notes">Invoice Notes</label>
          <div id="invoice_notes">{{ invoiceNotes }}</div>
        </v-col>
      </v-row>
    </div>
  </v-card>
</template>

<style>
#invoice_notes {
  border: 1px solid grey;
}

.labels {
  font-weight: 700;
}
</style>
