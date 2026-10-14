<script setup lang="ts">
import { onMounted, ref } from "vue";
import {
  NButton,
  NInput,
  NInputNumber,
  useMessage,
  NSelect,
  NCard,
  NTag,
  NTable,
  NDataTable,
} from "naive-ui";

onMounted(() => {
  message.create("WELCOME GUEST!");
});
const message = useMessage();
const vendorName = ref<string | null>(null);
const vendorPrice = ref<number | null>(null);
type status = "submitted" | "pending";
interface Vendor {
  name: string;
  price: number;
  status: status;
}
const vendorsQuotation = ref<Vendor[]>([
  {
    name: "Grand Marina Hotel",
    price: 10000,
    status: "submitted",
  },
  {
    name: "Sunset Bay & Resort",
    price: 15000,
    status: "submitted",
  },
  {
    name: "GlobalVisa",
    price: 20000,
    status: "pending",
  },
  {
    name: "CityLine",
    price: 25000,
    status: "pending",
  },
]);
const selectOption = [
  {
    label: "Submitted",
    value: "submitted",
  },
  {
    label: "Pending",
    value: "pending",
  },
];
const selectedStatus = ref<status>("submitted");
const addQuotation = (): void => {
  if (vendorPrice.value !== null && vendorPrice.value < 1) {
    message.error("Price should be greater than 0");
  } else if (vendorName.value?.trim() && vendorPrice.value !== null) {
    vendorsQuotation.value.push({
      name: vendorName.value.trim(),
      price: vendorPrice.value,
      status: selectedStatus.value,
    });
    vendorName.value = null;
    vendorPrice.value = null;
    message.success("Vendor Quotation is added");
  } else {
    message.error("Please enter both name and price of the vendor");
  }
};
const columns = [
  {
    title: "Vendor Name",
    key: "name",
  },
  {
    title: "Price of Vendor",
    key: "price",
  },
  {
    title: "Submission status",
    key: "status",
  },
];
</script>

<template>
  <div class="p-10 flex flex-col gap-5 mx-50 mt-20 border">
    <label for="name">Vendor Name : </label>
    <n-input id="name" v-model:value="vendorName"></n-input>
    <label for="price">Price : </label>
    <n-input-number id="price" v-model:value="vendorPrice"></n-input-number>
    <label for="status">Submission status : </label>
    <n-select
      :options="selectOption"
      v-model:value="selectedStatus"
      id="status"
    ></n-select>
    <n-button @click="addQuotation">Add Quotation</n-button>
    <n-data-table :columns="columns" :data="vendorsQuotation"></n-data-table>
  </div>
</template>
