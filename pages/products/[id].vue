<template>
  <div>
    <ProductDetails :product="product" />
  </div>
</template>

<script setup>
import ProductDetails from "../../components/ProductDetails.vue";

const { id } = useRoute().params;
const uri = "https://fakestoreapi.com/products/" + id;

//  fetch the products
const { data: product } = await useFetch(uri, { key: id });

if (!product) {
  throw createError({
    statusCode: 404,
    statusMessage: "product not found",
    fatal: true,
  });
}

definePageMeta({
  layout: "products",
});
</script>
