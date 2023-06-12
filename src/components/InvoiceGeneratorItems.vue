<script setup lang="ts">
defineProps<{
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
  invoiceTotals: { discount_total?: number; tax_total?: number; total?: number }
  calculateTotal: number
  itemsDiscountTotal: number
  itemsTaxTotal: number
  addItem: (index) => void
  removeItem: (index) => void
  invoiceItemTotal: (index) => void
}>()
</script>

<template>
  <v-row>
    <v-col md="12">
      <h2 className="mb-6">Items:</h2>
      <table className="w-100">
        <thead>
          <tr>
            <th class="text-left">No.</th>
            <th class="text-left">Desciption</th>
            <th class="text-left">Qty</th>
            <th class="text-left">Price</th>
            <th class="text-left">Discount %</th>
            <th class="text-left">Discount Amount</th>
            <th class="text-left">Tax %</th>
            <th class="text-left">Tax Amount</th>
            <th class="text-left">Total</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in invoiceItems" :key="index">
            <td class="item-index">{{ index + 1 }}</td>
            <td>
              <v-text-field v-model="item.description" variant="solo"></v-text-field>
            </td>
            <td>
              <v-text-field
                v-model.number="item.qty"
                @blur="invoiceItemTotal(index)"
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-text-field
                v-model.number="item.price"
                @blur="invoiceItemTotal(index)"
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-text-field
                v-model.number="item.discount"
                @blur="invoiceItemTotal(index)"
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-text-field
                v-model.number="item.discount_amount"
                @blur="invoiceItemTotal(index)"
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-text-field
                v-model.number="item.tax"
                @blur="invoiceItemTotal(index)"
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-text-field
                v-model.number="item.tax_amount"
                @blur="invoiceItemTotal(index)"
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-text-field
                height="24px"
                :value="item.total"
                readonly
                variant="solo"
              ></v-text-field>
            </td>
            <td>
              <v-btn color="primary" class="item-button" @click="removeItem(index)">
                <v-icon icon="mdi-minus" />
              </v-btn>
            </td>
          </tr>
        </tbody>
      </table>
      <v-btn color="primary" class="item-button" @click="addItem(index)">
        <v-icon>mdi-plus</v-icon>
        Add Item
      </v-btn>
      <v-row justify="end">
        <v-col cols="5">
          <table id="totals_table">
            <tbody>
              <tr>
                <td class="labels border_bottom">Discount:</td>
                <td class="labels border_bottom">{{ itemsDiscountTotal }}</td>
              </tr>
              <tr>
                <td class="labels border_bottom">Tax:</td>
                <td class="labels border_bottom">{{ itemsTaxTotal }}</td>
              </tr>
              <tr>
                <td class="labels border_bottom">Total:</td>
                <td class="labels border_bottom">{{ calculateTotal }}</td>
              </tr>
            </tbody>
          </table>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>

<style>
.labels {
  font-weight: 700;
}
.item-index {
  padding-bottom: 22px;
}
.item-button {
  margin-bottom: 22px;
  margin-left: 5px;
  padding: 1rem;
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
#totals_table {
  width: 100%;
}
#totals_table td:nth-child(2) {
  width: 40%;
}
#totals_table td {
  width: 20%;
}
#totals_table td:nth-child(2) {
  width: 40%;
}
</style>
