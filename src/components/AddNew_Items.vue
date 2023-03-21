<template>
  <div class="addnewdiv">
    
    <h1>Add New Items</h1>
    <div>
      <label>Name</label>
      <input type="text" v-model="productName" class="form-control" required />
      <p v-if="!productName">Please enter a name.</p>
    </div>
    <div>
      <label>Type</label>
      <input type="text" v-model="productType" class="form-control" required />
      <p v-if="!productType">Please enter a Type of item.</p>
    </div>
    <div>
      <label>Brand</label>
      <input type="text" v-model="brand" class="form-control" required />
      <p v-if="!brand">Please enter the item brand.</p>
    </div>
    <div>
      <label>Reviews</label>
 
      <input type="text" v-model="reviews" class="form-control" required />

    </div>
    <div>
      <label>Available Color</label>
      <input type="text" v-model="availableColor" class="form-control" required />
      <p v-if="!availableColor">Please enter the available colors.</p>
    </div>
    <div>
      <label for="image">Image</label>
      <input id="image" type="url" v-model="image" class="form-control" placeholder="Please Enter a URL for Image."
        required />
      <p v-if="isurlinvalid === true">Please enter valid URL for image.</p>
    </div>
    <h5>Specifications</h5>
    <div>
      <label>Point Size</label>
      <input type="text" v-model="specification.pointSize" class="form-control"
        placeholder="Please Enter a valid numerial value or  NA if not applicable." />
      <!-- <p v-if="isPointSizeValid === true">Please enter valid URL for image.</p> -->
    </div>

    <div>
      <label>Ink Color</label>
      <input type="text" v-model="specification.inkColor" class="form-control" />
    </div>
    <div>
      <label>Ink Type</label>
      <input type="text" v-model="specification.inkType" class="form-control" />
    </div>

    <div>
      <label for="waterproof">Waterproof</label>
      <input type="radio" id="waterproof-yes" name="waterproof" value="Yes" v-model="specification.waterProof" />
      <label for="Yes">Yes</label>
      <input type="radio" id="waterproof-no" name="waterproof" value="No" v-model="specification.waterProof" />
      <label for="No">No</label>
    </div>
    <button @click="addNew" :disabled="!isValid" class="btn btn-primary mt-3">
      Add New
    </button>
  </div>
</template>
  
  
<script>
import axios from "axios";
const API_URL = "https://educateddelectablepascal.cykistanis.repl.co/";

export default {
  data: function () {
    return {
      productName: "",
      productType: "",
      brand: "",
      reviews: [],
      availableColor: "",
      image: "",
      specification: {
        pointSize: "",
        inkColor: "",
        inkType: "",
        waterProof: "",
      },
      isurlinvalid: false,
      isPointSizeInvalid: false,
      // isProductNameInvalid: false,
    };
  },

  methods: {
    async addNew() {
      /* eslint-disable */
      const response = await axios.post(API_URL + "test_stationery", {
        productName: this.productName,
        productType: this.productType,
        brand: this.brand,
        reviews: this.reviews,
        availableColor: this.availableColor,
        image: this.image,
        pointSize: this.specification.pointSize,
        inkColor: this.specification.inkColor,
        inkType: this.specification.inkType,
        waterProof: this.specification.waterProof,
      });
      this.$emit("add-new-items");
    },
  },

  watch: {
    

    image(newImage) {
      const urlRegex = /^(ftp|http|https):\/\/[^ "]+$/;
      this.isurlinvalid = urlRegex.test(newImage);
    },
    "specification.pointSize"(newInput) {
      const pointInput = /^(\d+(?:\.\d+)?|NA)$/;
      this.isPointSizeInvalid = pointInput.test(newInput);
    },
  },
  computed: {
    isValid() {
      return (
        this.productName &&
        this.productType &&
        this.brand &&
        this.availableColor &&
        this.isurlinvalid &&
        this.isPointSizeInvalid === true
      );
    },
  },
};
</script>
  
  
<style scoped></style>