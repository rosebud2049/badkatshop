<template>
  <div class="flex justify-center m-6">
    <div v-if="this.illustration !== null">
      <div class="flex flex-col items-center border rounded-lg bg-gray-100">
        <div class="w-full bg-white rounded-lg flex justify-center">
          <img :src="illustration.image[0].formats.small.url" width="375" />
        </div>
        <div class="w-full bg-white rounded-lg flex justify-center"></div>
        <div class="w-full p-5 flex flex-col justify-between">
          <div>
            <h4
              class="mt-1 font-semibold text-lg leading-tight truncate text-gray-700"
            >
              {{ illustration.title }}
            </h4>
            <div class="mt-1 text-gray-600">{{ illustration.description }}</div>
          </div>

          <button
            class="snipcart-add-item mt-4 bg-white border border-gray-200 d hover:shadow-lg text-gray-700 font-semibold py-2 px-4 rounded shadow"
            :data-item-id="illustration.id"
            :data-item-price="illustration.price"
            :data-item-url="`${storeUrl}${this.$route.fullPath}`"
            :data-item-description="illustration.description"
            :data-item-name="illustration.title"
          >
            Add to cart
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  data() {
    return {
      illustration: null,
      storeUrl: process.env.storeUrl,
      fullPath: this.$route.fullPath,
    };
  },
  apollo: {
    illustration: {
      query: gql`
        query illustration($id: ID!) {
          illustration(id: $id) {
            id
            title
            description
            price
            image {
              formats
            }
          }
        }
      `,
      variables() {
        return {
          id: this.$route.params.id,
        };
      },
    },
  },
};
</script>

<style>
</style>
