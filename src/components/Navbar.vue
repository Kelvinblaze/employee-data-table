<template>
  <nav class="tw-bg-white tw-border-b tw-border-gray-100">
    <div class="stable-alignment">
      <div class="tw-py-3 tw-flex tw-items-center tw-justify-between">
        <Logo />

        <div class="tw-w-max">
          <div
            class="tw-bg-[#F8F8F8] tw-rounded-full tw-p-2 tw-flex tw-items-center tw-space-x-2"
          >
            <!-- Character Avatar -->
            <div
              class="tw-bg-[#13C1F0] tw-w-[30px] tw-h-[30px] tw-rounded-full tw-grid tw-place-content-center"
            >
              <div>
                <span class="tw-text-sm tw-text-white tw-font-medium">KO</span>
              </div>
            </div>

            <!-- User full name -->
            <div>
              <p class="tw-text-sm tw-text-primary tw-font-semibold">
                Kelvin Ossai
              </p>
              <p class="tw-text-xs">Administrator</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import Logo from "./Logo.vue";
</script>

<style lang="scss" scoped></style>
