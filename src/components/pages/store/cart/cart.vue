<template>
  <vf-o-layout>
    <vf-t-store-cart :cart="cart" />
  </vf-o-layout>
</template>
<script>
import { mapGetters } from "vuex";
import cartGetGql from "./cart.graphql";
export default {
  head() {
    return {
      title: this.$t("pages.store.cart.metaTitle")
    };
  },
  breadcrumbs() {
    return [
      {
        title: this.$t("pages.store.cart.breadcrumbTitle"),
        to: this.$route.path
      }
    ];
  },
  computed: {
    ...mapGetters({
      cart: "store/cart/get"
    })
  },
  async fetch(ctx) {
    await ctx.store.dispatch("apollo/query", {
      query: cartGetGql
    });

    if (
      !ctx.store.getters["vuefront/error"] &&
      ctx.store.getters["apollo/get"].cart
    ) {
      ctx.store.commit(
        "store/cart/setCart",
        ctx.store.getters["apollo/get"].cart
      );
    }
  }
};
</script>