<template>
  <section class="product-option">
    <div v-for="(option, index) in product.options" :key="index" class="mb-5 mt-3">
      <vf-m-product-option-checkbox
        v-if="option.type === 'checkbox'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-date
        v-else-if="option.type === 'date'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-datetime
        v-else-if="option.type === 'datetime'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-file
        v-else-if="option.type === 'file'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-radio
        v-else-if="option.type === 'radio'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-select
        v-else-if="option.type === 'select'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-text
        v-else-if="option.type === 'text'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-textarea
        v-else-if="option.type === 'textarea'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
      <vf-m-product-option-time
        v-else-if="option.type === 'time'"
        :option="option"
        :selected="options"
        @change="handleOptionChange($event, option)"
      />
    </div>
  </section>
</template>
<script>
import { isEmpty, filter } from "lodash";
import { mapGetters } from "vuex";
export default {
  props: ["product"],
  computed: {
    ...mapGetters({
      options: "store/product/options"
    })
  },
  methods: {
    checkActive(e, option) {
      let result = filter(
        this.options,
        value => value.id === option.id && e === value.value
      );

      return !isEmpty(result);
    },
    handleOptionChange(e, option) {
      let result = filter(this.options, value => value.id !== option.id);
      result.push({
        id: option.id,
        value: e
      });

      this.$store.commit("store/product/setOptions", result);
    }
  }
};
</script>