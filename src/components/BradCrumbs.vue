<template>
    <div class="brad-crumbs srUi">
      <ul>
        <template v-for="(bradCrumb,index) in BradCrumbs">
          <li :key="index" :class="BradCrumbs.length === index + 1 ? 'current' : ''">{{ bradCrumb }}</li>
  
          <li :key="index+'.'"  v-if="BradCrumbs.length !== index + 1"> /</li>
        </template>
  
      </ul>
  
    </div>
  </template>
  
  <script>
  export default {
    name: "BradCrumbs",
    props: {
      BradCrumbs: {
        required: true,
        type: Array,
      }
    }
  }
  </script>
  
  <style scoped>
  .brad-crumbs {
    display: flex;
    width: 100%;
    gap: 10px
  }
  
  .brad-crumbs ul {
    color: #727783;
    text-decoration: none;
    font-size: 16px;
    list-style:none;
    list-style-position:inside;
    display:flex;
    gap:10px;
    padding-left: 0;
  }
  
  .brad-crumbs li.current {
    color: black;
  }
  </style>