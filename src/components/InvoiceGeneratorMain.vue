<script setup lang="ts">
import { computed, reactive, ref } from 'vue'
import * as html2pdf from 'html2pdf.js'
import '@vuepic/vue-datepicker/dist/main.css'
import InvoiceGeneratorHeader from './InvoiceGeneratorHeader.vue'
import InvoiceGeneratorItems from './InvoiceGeneratorItems.vue'
import InvoiceGeneratorBankDetails from './InvoiceGeneratorBankDetails.vue'
import InvoiceTemplate from '@/components/InvoiceTemplate.vue'

const date = ref('')
let showPreview = false
const invoiceHeader = ref({
  businessName: '',
  from_taxNumber: '',
  from_address1: '',
  from_address2: '',
  from_city: '',
  from_postcode: '',
  clientName: '',
  client_taxNumber: '',
  client_address1: '',
  client_address2: '',
  client_city: '',
  client_postcode: '',
  invoice_id: '',
  invoice_date: '',
  purchase_order: '',
  invoice_due: ''
})

const invoiceTotals = ref({
  discount_total: 0,
  tax_total: 0,
  total: 0
})

const bankDetails = ref({
  bank_name: '',
  bank_account: '',
  swift_code: ''
})

const invoiceNotes = ref('')

const invoiceItems = reactive([
  {
    description: '',
    qty: 0,
    price: 0,
    discount: 0,
    tax: 0,
    discount_amount: 0,
    tax_amount: 0,
    total: 0
  }
])

const calculateTotal = computed(() => {
  return invoiceItems.reduce((acc, item) => acc + item.total, 0)
})

const itemsDiscountTotal = computed(() => {
  return invoiceItems.reduce((acc, item) => acc + item.discount_amount, 0)
})

const itemsTaxTotal = computed(() => {
  return invoiceItems.reduce((acc, item) => acc + item.tax_amount, 0)
})

const addItem = function (index) {
  invoiceItems.splice(index + 1, 0, {
    description: '',
    qty: '',
    price: '',
    discount: '',
    tax: '',
    discount_amount: '',
    tax_amount: '',
    total: ''
  })
}
const removeItem = function (index) {
  if (index > 0) invoiceItems.splice(index, 1)
}

const invoiceItemTotal = function (index) {
  let itemDiscounted
  let taxTotal
  let taxDiscountTotal
  //Item without tax and discount
  const calculatedTotal = invoiceItems[index].qty * invoiceItems[index].price
  invoiceItems[index].total = calculatedTotal

  //Discount applied
  if (invoiceItems[index].discount) {
    itemDiscounted = calculatedTotal * ((100 - invoiceItems[index].discount) / 100)
    invoiceItems[index].discount_amount = calculatedTotal * (invoiceItems[index].discount / 100)
    invoiceItems[index].total = itemDiscounted
  } else if (invoiceItems[index].discount === 0 || invoiceItems[index].discount === '') {
    invoiceItems[index].discount_amount = 0
  }
  // If tax applied.
  if (invoiceItems[index].tax) {
    taxTotal = calculatedTotal * (invoiceItems[index].tax / 100)
    invoiceItems[index].tax_amount = taxTotal
    invoiceItems[index].total = taxTotal + calculatedTotal
  } else if (invoiceItems[index].tax === 0 || invoiceItems[index].tax === '') {
    invoiceItems[index].tax_amount = 0
  }
  // If tax & discount applied.
  if (invoiceItems[index].tax && invoiceItems[index].discount) {
    taxDiscountTotal = itemDiscounted * (invoiceItems[index].tax / 100)
    invoiceItems[index].discount_amount = calculatedTotal * (invoiceItems[index].discount / 100)
    invoiceItems[index].tax_amount = taxDiscountTotal
    invoiceItems[index].total = itemDiscounted + taxDiscountTotal
  }
}

const printWindow = function () {
  const element = document.getElementById('invoice_template').innerHTML
  document.body.innerHTML = element
  window.print()
  window.location.reload()
}

const printToPDF = function () {
  const element = document.getElementById('invoice_template')
  const opt = {
    margin: 10,
    filename: 'invoice.pdf',
    image: { type: 'jpeg', quality: 1 },
    html2canvas: { scale: 2, scrollX: 0, scrollY: 0 }
  }
  html2pdf().from(element).set(opt).save()
}
const preview = function () {
  this.showPreview = true
  window.scroll(0, 0)
}

const editInvoice = function () {
  showPreview = false
}
</script>

<template>
  <div id="title_container">
    <div id="main_title_wrapper">
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
      <div>
        <h1 className="font-weight-bold">Invoice Generator</h1>
        <h2>InvoiceTea for your Invoice Team</h2>
      </div>
    </div>
  </div>
  <div class="action_buttons">
    <v-btn color="white" invert @click="editInvoice()">Back</v-btn>
    <v-btn color="primary" @click="printWindow()">Print to PDF</v-btn>
    <v-btn color="primary" @click="printToPDF()">Save PDF</v-btn>
  </div>
  <div v-if="!showPreview" id="card_wrapper" className="flex justify-self-center">
    <v-form d-flex>
      <v-card class="ma-12 pa-16" raised elevation="12">
        <v-row>
          <h2 id="invoice_title">Invoice</h2>
        </v-row>
        <InvoiceGeneratorHeader :invoice-header="invoiceHeader" />
        <InvoiceGeneratorItems
          :invoice-items="invoiceItems"
          :invoice-totals="invoiceTotals"
          :calculate-total="calculateTotal"
          :items-discount-total="itemsDiscountTotal"
          :items-tax-total="itemsTaxTotal"
          :add-item="addItem"
          :remove-item="removeItem"
          :invoice-item-total="invoiceItemTotal"
        />
        <InvoiceGeneratorBankDetails :bank-details="bankDetails" />
        <v-row>
          <v-col>
            <label for="Invoice Notes">Invoice Notes</label>
            <v-textarea
              solo
              name="input-7-4"
              v-model="invoiceNotes"
              placeholder="Something important"
            ></v-textarea>
          </v-col>
        </v-row>
        <v-btn @click="preview" color="primary">Preview</v-btn>
      </v-card>
    </v-form>
  </div>
  <v-layout>
    <v-navigation-drawer
      color="#B19FDF"
      id="navigation_drawer"
      expand-on-hover
      rail
      right
      permanent
      dark
    >
      <v-list>
        <v-list-item
          alt="Vue logo"
          class="logo"
          prepend-avatar="@/assets/logo.svg"
          title="Invoice Generator"
        ></v-list-item>
        <v-divider></v-divider>
        <v-list-item
          prepend-icon="mdi-cloud-print-outline"
          title="Print to PDF"
          value="myfiles"
          @click="printWindow()"
        ></v-list-item>
        <v-list-item
          prepend-icon="mdi-content-save-all"
          title="Save PDF"
          value="shared"
          @click="printToPDF()"
        ></v-list-item>
        <v-list-item
          prepend-icon="mdi-square-edit-outline"
          title="Edit"
          value="starred"
          @click="editInvoice()"
        ></v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main style="height: 500px"></v-main>
  </v-layout>
  <InvoiceTemplate
    :bank-details="bankDetails"
    :invoice-header="invoiceHeader"
    :invoice-items="invoiceItems"
    :invoice-totals="invoiceTotals"
    :invoice-item-total="invoiceItemTotal"
    :calculate-total="calculateTotal"
    :items-discount-total="itemsDiscountTotal"
    :items-tax-total="itemsTaxTotal"
    :invoice-notes="invoiceNotes"
    id="invoice_template"
  />
</template>

<style>
//Titles
#title_container {
  display: flex;
  align-items: center;
}

#main_title_wrapper {
  display: flex;
  align-items: center;
  gap: 2rem;
  margin-left: 3rem;
  padding: 1rem;
}

.action_buttons {
  display: flex;
  justify-content: end;
  gap: 1rem;
  margin-right: 3rem;
}

#invoice_title {
  font-size: 2rem;
  padding-left: 2rem;
}

#invoice_notes {
  border: 1px solid grey;
}

button,
input,
select,
textarea {
  background-color: transparent;
  border-style: border solid 1px;
}
</style>
