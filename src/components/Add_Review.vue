<template>
  
  <div>
     
    <h1>Add in review</h1>
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
    <div>
      <label>Available Color</label>
      <input type="text" v-model="availableColor" class="form-control" />
    </div>
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
      <label>Review</label>
      <input type="text" v-model="reviews" class="form-control" />
      <!-- <p>Reviews Array: {{ reviewsArray }}</p> -->
    </div>
    <div>
      <button class="btn btn-primary mt-3" @click="submitReview">
        Submit Review
      </button>
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
    this.availableColor = response.data.availableColor;
    this.reviews = response.data.reviews || [];
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
      availableColor: "",
      reviews: [],
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
    /* eslint-disable */
    async submitReview(itemId) {
      /* eslint-disable */
      
      const newReviews = this.reviews.split(",");
      const response = await axios.patch(
        API_URL + "test_stationery/" + this.itemId + "/reviews",
        {
          reviews: newReviews,
        }
      );
      this.reviews = newReviews; // set the reviews data to the new array
this.$emit("reviewadded");
      
    },
  },
  computed: {
    reviewsArray() {
  return this.reviews.split(' ');
}
  }
};
</script>



<style scoped>
</style>