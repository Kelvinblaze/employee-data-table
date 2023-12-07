<template>
  <!-- Custom Loader for data fetching -->
  <Loader :loading="isLoading" />

  <main class="tw-bg-[#F8F8F8] tw-min-h-screen tw-w-full">
    <!-- Main Navigation Bar for Header -->
    <Navbar />

    <div class="tw-grid tw-grid-cols-12">
      <!-- For Side Navigation -->
      <aside
        class="tw-bg-teal-950 tw-h-screen tw-col-span-12 lg:tw-col-span-1 tw-hidden lg:tw-block"
      ></aside>

      <section class="tw-col-span-12 lg:tw-col-span-11">
        <!-- Top Header -->
        <div class="tw-bg-white tw-px-10 tw-border-b tw-border-gray-100">
          <div class="tw-flex tw-items-center tw-justify-between tw-py-5">
            <h5 class="tw-text-2xl tw-font-semibold">Employee</h5>

            <!-- Call to Action to add Employee -->
            <button class="btn-primary">Add Employee</button>
          </div>

          <!-- Menu Tab Item List -->
          <div class="">
            <ul class="tw-flex tw-items-center tw-space-x-5 tw-text-teal-900">
              <li
                class="tw-py-2 tw-border-b-2 tw-border-teal-900 tw-cursor-pointer"
              >
                List of employees
              </li>
              <li
                class="tw-py-2 hover:tw-border-b-2 hover:tw-border-teal-900 tw-cursor-pointer"
              >
                Employee hours
              </li>
            </ul>
          </div>
        </div>

        <!-- Filters  -->
        <div class="tw-px-10 tw-py-10">
          <!-- Search -->
          <form
            action=""
            class="tw-flex tw-justify-end tw-items-center tw-space-x-5"
          >
            <div class="form-group">
              <input
                type="text"
                class="custom-input"
                placeholder="Search by name"
                v-model="search"
              />
            </div>

            <div class="form-group">
              <select class="custom-select" v-model="status">
                <option value="" disabled selected>- Select Status -</option>
              </select>
            </div>

            <div class="form-group">
              <select class="custom-select" v-model="resposibility">
                <option value="" disabled selected>
                  - Select Responsibility -
                </option>
              </select>
            </div>

            <div class="form-group">
              <select class="custom-select" v-model="department">
                <option value="" disabled selected>
                  - Select Department -
                </option>
              </select>
            </div>

            <div class="form-group">
              <button type="submit" class="btn-primary">Filter</button>
            </div>
          </form>
        </div>

        <!-- Table -->

        <div v-if="isError">
          <div
            class="tw-min-h-[284px] tw-px-8 tw-pt-10 tw-pb-12 tw-flex tw-flex-col tw-gap-6 tw-justify-center tw-items-center tw-w-full"
          >
            <img
              src="https://cdn0.iconfinder.com/data/icons/shift-free/32/Error-1024.png"
              alt="error"
              class="tw-w-[80px] tw-h-[80px] tw-text-center tw-m-auto"
            />

            <div>
              <h3
                class="tw-text-center tw-text-gray-900 tw-text-base tw-font-semibold tw-leading-normal"
              >
                An Error Occurred
              </h3>
              <p
                class="tw-max-w-[352px] tw-text-center tw-text-gray-500 tw-text-sm tw-font-normal tw-leading-tight"
              >
                {{ error }}
              </p>
            </div>

            <button @click="refetch" :disabled="isFetching" class="btn-primary">
              {{ isFetching ? "Refetching..." : "Refetch" }}
            </button>
          </div>
        </div>
        <div v-else class="tw-overflow-x-auto tw-w-full tw-px-10">
          <table class="tw-table tw-min-w-full tw-bg-white tw-border">
            <thead>
              <tr
                class="tw-uppercase tw-bg-white tw-border-b tw-text-gray-500 tw-text-xs tw-font-medium tw-leading-[18px] tw-text-left"
              >
                <th scope="col" class="tw-px-6 tw-py-3">
                  <span> Name </span>
                </th>
                <th scope="col" class="tw-px-6 tw-py-3">Position</th>
                <th scope="col" class="tw-px-6 tw-py-3">Department</th>
                <th scope="col" class="tw-px-6 tw-py-3">Start of Contract</th>
                <th scope="col" class="tw-px-6 tw-py-3">Status</th>
              </tr>
            </thead>
            <tbody>
              <tr
                class="tw-border-b tw-text-xs"
                v-for="(employee, i) in employees.data"
                :key="employee.id"
              >
                <td
                  class="tw-px-6 tw-py-3 tw-whitespace-nowrap tw-flex tw-items-center tw-space-x-2"
                >
                  <div class="tw-w-[30px] tw-h-[30px] tw-rounded-full">
                    <img
                      v-if="employee.user.avatar === null"
                      :src="avatar"
                      :alt="employee.user.first_name"
                      class="tw-w-full tw-h-full tw-object-cover tw-rounded-full"
                    />
                    <img
                      v-else
                      :src="employee.user.avatar"
                      :alt="employee.user.first_name"
                      class="tw-w-full tw-h-full tw-object-cover tw-rounded-full"
                    />
                  </div>

                  <div class="tw-text-xs">
                    <p class="tw-font-semibold tw-text-teal-900">
                      {{ employee.user.first_name }}
                      {{ employee.user.last_name }}
                    </p>
                    <p>{{ employee.user.email }}</p>
                  </div>
                </td>
                <td
                  class="tw-px-6 tw-py-3 tw-whitespace-nowrap tw-text-teal-900"
                >
                  {{ employee.position[0].positions_id.name }}
                </td>

                <td class="tw-px-6 tw-py-3 tw-whitespace-nowrap">
                  {{ employee.company.trade_name }}
                </td>
                <td class="tw-px-6 tw-py-3 tw-whitespace-nowrap">
                  {{
                    moment(employee.current_contract.entry_date).format(
                      "DD, MMM YYYY"
                    )
                  }}
                </td>
                <td class="tw-px-6 tw-py-3 tw-whitespace-nowrap">
                  <div
                    class="tw-capitalize tw-text-xs tw-bg-green-100 tw-text-green-500 tw-py-1 tw-px-2 tw-rounded-full tw-w-max"
                  >
                    {{ employee.user.status }}
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Pagination -->
        <section class="tw-p-10">
          <div class="tw-text-xs">
            <p>Showing 1 to {{ limit }} of results.</p>
          </div>

          <div></div>
        </section>
      </section>
    </div>
  </main>
</template>

<script setup>
import Navbar from "./components/Navbar.vue";
import Loader from "./components/Loader.vue";
import avatar from "./assets/images/avatar.svg";
import moment from "moment";
import { ref } from "vue";

import { useQuery } from "vue-query";

const limit = 5;
const search = ref("");
const status = ref("");
const department = ref("");
const resposibility = ref("");

const fetcher = async () => {
  const token = import.meta.env.VITE_DIRECTUS_TOKEN; // Replace this with your actual Bearer token

  const response = await fetch(
    `https://staging-backend.teamwell.co/items/employees?limit=${limit}&fields=*.*.*`,
    {
      method: "GET",
      headers: {
        Authorization: `Bearer ${token}`,
      },
    }
  );

  return response.json();
};

const {
  isLoading,
  isError,
  isFetching,
  data: employees,
  error,
  refetch,
} = useQuery("employees", fetcher);

console.log(employees.value);
</script>

<style lang="scss" scoped>
.router-link-active li {
  border: 1px solid red;
}
</style>
