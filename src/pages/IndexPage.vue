<template>
  <div class="container">
    <BradCrumbs :brad-crumbs="BradCrumbs" />
    <h1 class="catalogue-title srUi600">Комплекты стеллажных систем</h1>
    <FiltersPart @sort="sortItems($event)" @filter="filterItems($event)" />
    <section class="section-products">
      <div class="container">
        <div class="row row-gap-4">
          <div
            class="col-md-6 col-lg-4 col-xl-3"
            v-for="item in filteredItems"
            :key="item.id"
          >
            <ProductPart :product="item" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import ProductPart from "@/components/ProductPart";
import BradCrumbs from "@/components/BradCrumbs";
import FiltersPart from "@/components/FiltersPart";
import items from "../json/items.json";

export default {
  name: "IndexPage",
  components: { ProductPart, BradCrumbs, FiltersPart },
  data() {
    return {
      filterSort: false,
      filterMaterial: false,
      filter: [],
      BradCrumbs: [
        "Главная",
        "Системы хранения",
        "Комплекты стеллажных систем",
      ],
    };
  },
  computed: {
    products() {
      return items;
    },
    filteredItems() {
      if (
        (!this.filterSort || this.filterSort === "default") &&
        (!this.filterMaterial || this.filterMaterial === "default")
      ) {
        return this.products;
      }

      if (this.filterMaterial) {
        return this.sortedProducts(this.filterByMaterial());
      }

      return this.sortedProducts(this.products);
    },
  },
  methods: {
    sortItems(key) {
      this.filterSort = key;
    },
    filterItems(key) {
      this.filterMaterial = key;
    },
    sortedProducts(itemsForSort) {
      return itemsForSort.slice().sort((a, b) => {
        if (this.filterSort === "priceUp") {
          return a.price.current_price - b.price.current_price;
        } else if (this.filterSort === "priceDown") {
          return b.price.current_price - a.price.current_price;
        }
      });
    },
    filterByMaterial() {
      if (this.filterMaterial === "default") {
        return this.products;
      }
      this.filter = [...this.products];
      return this.filter.filter((item) => item.material == this.filterMaterial);
    },
  },
};
</script>

<style scoped>
.catalogue-title {
  color: black;
  font-size: 36px;
  font-weight: 600;
  line-height: 48px;
  word-wrap: break-word;
  margin-top: 32px;
  text-align: left;
}
</style>
