<template>
  <div class="select-block">
    <label class="select-block__label srUi">{{ caption }}</label>
    <select v-model="val">
      <option
        v-for="option in options"
        :value="option[itemKey]"
        :key="option[itemKey] + option.name"
      >
        {{ option.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "CustomSelect",
  props: {
    options: {
      type: Array,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    caption: {
      type: String,
      required: "",
    },
    itemKey: {
      default: "key",
    },
  },
  data() {
    return {
      isOpen: false,
      val: this.value,
    };
  },
  methods: {
    toggleDropdown() {
      this.isOpen = !this.isOpen;
    },
    selectOption(option) {
      this.$emit("input", option);
      this.isOpen = false;
    },
  },
  computed: {
    selected() {
      return this.options.find((item) => item[this.itemKey] === this.value);
    },
  },
  watch: {
    val() {
      this.$emit("input", this.val);
    },
    value() {
      this.val = this.value;
    },
  },
};
</script>

<style scoped>
.select-block select {
  width: 100%;
  height: 40px;
  background-color: #f2f2f2;
  border: none;
  border-radius: 0px;
  padding: 0 15px;
}
.select-block select:active,
.select-block select:focus {
  border: none;
  outline: none;
}

.select-block {
  display: inline-block;
  position: relative;
  width: 100%;
}

.select-block__label {
  margin-bottom: 6px;
  margin-left: 16px;
  display: block;
  color: #4f4f4f;
  font-size: 12px;
  font-weight: 400;
  line-height: 18px;
  letter-spacing: 0.36px;
  word-wrap: break-word;
}
</style>
