<template>
    <div>
      <h1>Edit items</h1>
      <div>
        <label>Product Name</label>
        <input type="text" v-model="productName" class="form-control" />
      </div>
      <div>
        <label>Product Type</label>
        <input type="text" v-model="productType" class="form-control" />
      </div>
      <div>
        <label>Brand</label>
        <input type="text" v-model="brand" class="form-control" />
      </div>
      <!-- <div>
        <label>Available Color</label>
        <input type="text" v-model="availableColor" class="form-control" />
      </div> -->
      <div>
        <label>Image</label>
        <input type="url" v-model="image" class="form-control" />
      </div>
      <h5>Specifications</h5>
      <div>
        <label>Point Size</label>
        <input
          type="text"
          v-model="specification.pointSize"
          class="form-control"
        />
      </div>
      <div>
        <label>Ink Color</label>
        <input
          type="text"
          v-model="specification.inkColor"
          class="form-control"
        />
      </div>
      <div>
        <label>Ink Type</label>
        <input type="text" v-model="specification.inkType" class="form-control" />
      </div>
      <div>
        <!-- <label>Waterproof</label>
        <input
          type="text"
          v-model="specification.waterProof"
          class="form-control"
        /> -->
        <label for="waterproof">Waterproof</label>
        <input
          type="radio"
          name="waterproof"
          value="Yes"
          v-model="specification.waterProof"
        />
        <label for="Yes">Yes</label>
        <input
          type="radio"
          name="waterproof"
          value="No"
          v-model="specification.waterProof"
        />
        <label for="No">No</label>
      </div>
      <div>
        <button class="btn btn-primary mt-3" @click="updateItem">Update</button>
      </div>
    </div>
  </template>
  
  
  <script>
  import axios from "axios";
  const API_URL = "https://educateddelectablepascal.cykistanis.repl.co/";
  export default {
    props: ["itemId"],
    async created() {
      const response = await axios.get(
        API_URL + "test_stationery/" + this.itemId
      );
      this.productName = response.data.productName;
      this.productType = response.data.productType;
      this.brand = response.data.brand;
      this.image = response.data.image;
      this.specification.pointSize = response.data.specification.pointSize;
      this.specification.inkColor = response.data.specification.inkColor;
      this.specification.inkType = response.data.specification.inkType;
      this.specification.waterProof = response.data.specification.waterProof;
    },
    data: function () {
      return {
        productName: "",
        productType: "",
        brand: "",
        image: "",
        specification: {
          pointSize: "",
          inkColor: "",
          inkType: "",
          waterProof: "",
        },
      };
    },
    methods: {
      async updateItem() {
        await axios.patch(API_URL + "test_stationery/" + this.itemId, {
          productName: this.productName,
          productType: this.productType,
          brand: this.brand,
          availableColor: this.availableColor,
          image: this.image,
          pointSize: this.specification.pointSize,
          inkColor: this.specification.inkColor,
          inkType: this.specification.inkType,
          waterProof: this.specification.waterProof,
        });
        this.$emit("items-edited");
      },
    },
  };
  </script>
  
  
  
  <style scoped>
  </style>