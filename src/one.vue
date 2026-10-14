<script setup lang="ts">
import { ref } from "vue";
import {
  NButton,
  NInput,
  useMessage,
  NSelect,
  NCard,
  NTag,
  NTable,
  NDataTable,
} from "naive-ui";

const message = useMessage();

const count = ref<number>(0);

function increaseCount(): void {
  count.value++;
}
function resetCount(): void {
  count.value = 0;
}
const vendorName = ref<string>("");
function saveVendor(): void {
  if (vendorName.value.trim() === "") {
    message.error("Please enter a vendor name");
  } else {
    message.success(`${vendorName.value} is added`);
  }
}
const vendors = [
  {
    label: "Grand Marina",
    value: "Grand Marina",
  },
  {
    label: "Sunset Bay & Resort",
    value: "Sunset Bay & Resort",
  },
  {
    label: "GlobalVisa",
    value: "GlobalVisa",
  },
  {
    label: "CityLine Transport",
    value: "CityLine Transport",
  },
];
const vendorsTable = [
  {
    name: "Grand Marina",
    price: 25000,
  },
  {
    name: "Sunset Bay & Resort",
    price: 20000,
  },
  {
    name: "GlobalVisa",
    price: 15000,
  },
  {
    name: "CityLine Transport",
    price: 30000,
  },
];
const selectedVendor = ref<string | null>(null);
interface Vendor {
  name: string;
  price: number;
}

const vendorData: Vendor[] = [
  {
    name: "Grand Marina",
    price: 25000,
  },
  {
    name: "Sunset Bay & Resort",
    price: 20000,
  },
  {
    name: "GlobalVisa",
    price: 15000,
  },
  {
    name: "CityLine Transport",
    price: 30000,
  },
];

const columns = [
  {
    title: "Vendor Name",
    key: "name",
  },
  {
    title: "Price",
    key: "price",
  },
];
</script>

<template>
  <div class="p-10">
    <h2>My First Naive UI Practice</h2>

    <p>Count: {{ count }}</p>

    <n-button type="primary" @click="increaseCount"> Increase Count </n-button>
    <br /><br />
    <n-button type="error" @click="resetCount">Reset</n-button>
    <br /><br />
    <n-input
      v-model:value="vendorName"
      placeholder="Enter vendor name..."
    ></n-input>
    <n-button type="primary" @click="saveVendor">Save Vendor</n-button>
    <br /><br />
    <n-select
      v-model:value="selectedVendor"
      :options="vendors"
      placeholder="Please select a vendor"
      clearable
      filterable
    ></n-select>
    <br />
    <hr />
    <br />
    <n-card title="Grand Marina" hoverable>
      <p>Category : Hotel</p>
      <p>Price : 25000</p>
    </n-card>
    <br />
    <hr />
    <br />
    <n-card title="SkyLine Travels" hoverable>
      <p>Category : Hotel</p>
      <p>Price : 18000</p>
      <n-tag type="success" round bordered>Submitted</n-tag><br /><br />
      <n-tag type="warning" round bordered>Pending</n-tag><br /><br />
      <n-tag type="error" round bordered>Declined</n-tag><br /><br />
    </n-card>
    <br />
    <hr />
    <br />
    <n-table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="obj in vendorsTable" key="obj.name">
          <td>{{ obj.name }}</td>
          <td>{{ obj.price }}</td>
        </tr>
      </tbody>
    </n-table>
    <br />
    <hr />
    <br />
    <n-data-table :columns="columns" :data="vendorData"></n-data-table>
  </div>
</template>
