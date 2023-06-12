<script setup lang="ts">
import { ref } from 'vue';
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'


const invoice = ref( {   businessName: "",
    from_taxnumber: "",
    from_address1: "",
    from_address2: "",
    from_city: "",
    from_postcode: "",
    clientName: "",
    client_taxnumber: "",
    client_address1: "",
    client_address2: "",
    client_city: "",
    client_postcode: "",
    invoice_id: "",
    invoice_date: "",
    purchase_order: "",
    invoice_due: "",
    items: [
    {
        description: "",
        qty: "",
        price: "",
        discount: "",
        tax: "",
        discount_amount: "",
        tax_amount: "",
        total: "",
    },
],
    discount_total: 0,
    tax_total: 0,
    total: 0,
    bank_name: "",
    bank_account: "",
    swift_code: "",
    invoice_notes: "",

})



// menu: false,
//     menu2: false,
//     showPreview: false,
//     drawer: true,
//     color: "blue",
//     colors: ["primary", "blue", "success", "red", "teal"],
//     right: true,
//     permanent: true,
//     miniVariant: false,
//     expandOnHover: true,
//     background: false,

</script>

<template>


</template>
