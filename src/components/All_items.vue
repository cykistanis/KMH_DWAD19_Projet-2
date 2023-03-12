<template>
    <div>
      <h1>All Items</h1>
      <input type="text" v-model="searchterms" id="headersty" />
      <br />
  
      <!-- dropdown option start here-->
      <label for="inkcolor">Select Ink color</label>
      <select name="inkcolor" v-model="searchbyink">
        <option value="">All Colours</option>
        <option value="Blue">Blue</option>
        <option value="Black">Black</option>
        <option value="Gold">Gold</option>
      </select>
      <!-- dropdown option end here-->
  
      <!-- checkbox for ink color start here -->
  
      <br />
  
      <!-- Radio btn for waterproof start here -->
      <label for="waterproof">Waterproof</label>
      <input
        type="radio"
        name="waterproof"
        value="yes"
        v-model="waterproofstatus"
      />
      <label for="yes">Yes</label>
      <input
        type="radio"
        name="waterproof"
        value="no"
        v-model="waterproofstatus"
      />
      <label for="no">No</label>
      <input type="radio" name="waterproof" value="" v-model="waterproofstatus" />
      <label for="">Reset</label>
  
      <!-- Radio btn for waterproof end here -->
  
      <div class="container text-left">
        <div class="row cards-container">
          <div
            v-for="p in filteredProducts"
            v-bind:key="p._id"
            class="card"
            style="width: 18rem"
          >
            <div class="col">
              <div class="card-body">
                <ul class="list-group list-group-flush">
                  <!-- <li>Product ID : {{ p._id }}</li> -->
                  <li class="list-group-item">Name : {{ p.productName }}</li>
                  <li class="list-group-item">Type : {{ p.productType }}</li>
                  <li class="list-group-item">Brand: {{ p.brand }}</li>
                  <li class="list-group-item">
                    Available Color: {{ p.availableColor }}
                  </li>
  
                  <li class="list-group-item">Specification</li>
                  <ul class="list-group list-group-flush">
                    <li class="list-group-item">
                      Point Size: {{ p.specification.pointSize }}
                    </li>
                    <li class="list-group-item">
                      Ink Color: {{ p.specification.inkColor }}
                    </li>
                    <li class="list-group-item">
                      Ink Type: {{ p.specification.inkType }}
                    </li>
                    <li class="list-group-item">
                      Waterproof: {{ p.specification.waterProof }}
                    </li>
                    <div class="list-group-item">
                      <button
                        type="button"
                        class="btn btn-info delbtn"
                        @click="addReview(p._id)"
                      >
                        Add Reviews
                      </button>
                    </div>
                    <li class="list-group-item">Reviews</li>
  
                    <ul class="list-group list-group-flush reviewsty">
                      <li
                        v-for="(review, index) in p.reviews"
                        :key="index"
                        class="list-group-item"
                      >
                        - {{ review }}
                      </li>
                    </ul>
                  </ul>
  
                  <img
                    class="container cardimg"
                    v-bind:src="p.image"
                    width="50px"
                  />
                </ul>
                <button
                  type="button"
                  class="btn btn-primary editbtn"
                  @click="editItems(p._id)"
                >
                  Edit
                </button>
                <button
                  type="button"
                  class="btn btn-danger ms-3 delbtn"
                  @click="deleteItem(p._id)"
                >
                  Delete
                </button>
  
                <br />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  
  
  <script>
  import axios from "axios";
  const API_URL = "https://educateddelectablepascal.cykistanis.repl.co/";
  
  export default {
    data: function () {
      return {
        items: [],
        searchterms: "",
        searchbyink: "",
        waterproofstatus: "",
      };
    },
  
    async created() {
      let response = await axios.get(API_URL + "test_stationery");
      this.items = response.data;
    },
    methods: {
      editItems(itemId) {
        this.$emit("edit-items", itemId);
      },
      addReview(itemId) {
        this.$emit("add-reviews", itemId);
      },
      // deleteItems(itemId) {
      //   this.$emit("delete-items", itemId);
      // },
      async deleteItem(itemId) {
        await axios.delete(API_URL + "test_stationery/" + itemId);
        this.items = this.items.filter((item) => item._id !== itemId);
      },
    },
    computed: {
      filteredProducts: function () {
        let filtered = [];
        for (let p of this.items) {
          if (
            p.productType
              .toLowerCase()
              .includes(this.searchterms.toLowerCase()) &&
            p.specification.inkColor
              .toLowerCase()
              .includes(this.searchbyink.toLowerCase()) &&
            p.specification.waterProof
              .toLowerCase()
              .includes(this.waterproofstatus.toLowerCase())
          ) {
            filtered.push(p);
          }
        }
        return filtered;
      },
      // filteredByInk: function () {
      //   let filtered = [];
      //   for (let p of this.items) {
      //     if (
      //       p.specification.inkColor
      //         .toLowerCase()
      //         .includes(this.searchbyink.toLowerCase())
      //     ) {
      //       filtered.push(p);
      //     }
      //   }
      //   return filtered;
      // },
    },
  };
  </script>
  
  <style scoped>
  @import url("https://fonts.googleapis.com/css2?family=Courgette&family=Gothic+A1:wght@200&family=Libre+Baskerville:ital@1&family=Marck+Script&family=Nanum+Myeongjo&family=Oleo+Script&family=Satisfy&family=Tangerine:wght@700&display=swap");
  #headersty {
    display: block;
  }
  
  .card-body {
    padding: 10px 0px 10px 0px;
    font-family: "Amaranth", sans-serif;
    font-size: 15px;
  }
  
  .cards-container {
    display: flex;
    justify-content: space-evenly;
    /* margin: 0px 2px 0px 2px; */
  }
  
  .card {
    width: 18rem;
    margin-bottom: 20px;
  }
  
  .editbtn {
    background-color: rgb(76, 185, 228);
  }
  </style>