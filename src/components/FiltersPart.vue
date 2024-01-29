<template>
    <div class="row mt-32">
      <div class="col-sm-4">
        <CustomSelect :options="sortOptions" v-model="sortOptionSelected" caption="Сортировать по:"/>
      </div>
      <div class="col-sm-4 ">
        <CustomSelect :options="materialsFilter" v-model="materialSelected" item-key="id" caption="Материал:"/>
      </div>
    </div>
  
  </template>
  
  <script>
  import CustomSelect from "@/components/CustomSelect";
  import materials from '@/json/materials.json';
  
  export default {
    components: {CustomSelect},
    name: "FiltersPart",
    data() {
      return {
        sortOptions: [
          {
            key: 'default',
            name: 'По умолчанию',
          },
          {
            key: 'priceUp',
            name: 'Цена по возрастанию ',
          },
          {
            key: 'priceDown',
            name: 'Цена по убыванию ',
          }
        ],
        materialsFilterItems: materials,
        sortOptionSelected: 'default',
        materialSelected: 'default',
      }
    },
    computed: {
      materialsFilter() {
        return materials;
      }
    },
    watch: {
      sortOptionSelected() {
        this.$emit('sort', this.sortOptionSelected);
      },
      materialSelected() {
        this.$emit('filter', this.materialSelected);
      }
    },
    created() {
      if (this.materialsFilterItems[0]?.id !== 'default') {
        this.materialsFilterItems.unshift({
          id: 'default',
          name: 'По умолчанию',
        })
      }
  
    }
  }
  </script>
  
  <style scoped>
  
  </style>