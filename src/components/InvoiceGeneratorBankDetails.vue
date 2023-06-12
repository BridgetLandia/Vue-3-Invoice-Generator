<script setup lang="ts">
defineProps<{
  bankDetails: {
    bank_name: string
    bank_account: string
    swift_code: string
  }
}>()
</script>

<template>
  <h2 className="mb-2">Bank Information:</h2>
  <v-row>
    <v-col cols="3">
      <v-text-field
        label="Bank Name"
        placeholder="Bank Name"
        v-model="bankDetails.bank_name"
        variant="solo"
      ></v-text-field
    ></v-col>
    <v-col cols="4">
      <v-text-field
        label="Account number"
        placeholder="02213425"
        v-model="bankDetails.bank_account"
        variant="solo"
      ></v-text-field>
    </v-col>
    <v-col cols="3">
      <v-text-field
        label="SWIFT Code"
        placeholder="SWIFT"
        v-model="bankDetails.swift_code"
        variant="solo"
      ></v-text-field>
    </v-col>
  </v-row>
</template>

<style></style>
