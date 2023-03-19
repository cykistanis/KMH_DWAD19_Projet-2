<template>
  <div id="maindiv">
    <div class="container">
      <nav class="navbar navbar-expand-sm navbar-dark">
        <div >
    <a class="navbar-brand" href="#">
      <img :src="require('@/assets/navlogo.png')" alt="Bootstrap" 
      class="navbarlogo"
      width="200" height="140">
    </a>
  </div>
        <div class="container-fluid">
          <!-- Links -->
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link" href="#" @click="goallitems">Stationery Hub</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="gonewitems">Contribute to the Collection</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="goaboutus">The Stationery Enthusiasts</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="gocontactus">Get in Touch</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="gologin">Sign In to Stationery World</a>
            </li>
          </ul>
        </div>
      </nav>
      <main>
        <About_us v-if="currentPage == 'aboutus'" />
        <All_items
          v-if="currentPage == 'allitems'"
          @edit-items="goedititems"
          @add-reviews="goaddReview"
          @delete-item="goallitems"
        />
        <Edit_Items
          v-if="currentPage == 'edit-items'"
          :itemId="itembeingEdited"
          @items-edited="goallitems"
        />
        <Add_Review
          v-if="currentPage == 'add-reviews'"
          :itemId="reviewadded"
          @review-added="goallitems"
        />
        <Contact_us v-if="currentPage == 'contactus'" />
        <Log_in v-if="currentPage == 'login'" />
        <AddNew_Items
          v-if="currentPage == 'addnewitems'"
          @add-new-items="goallitems"
        />
      </main>
    </div>
  </div>
</template>

<script>
import About_us from "./components/About_us";
import All_items from "./components/All_items";
import Contact_us from "./components/Contact_us";
import AddNew_Items from "./components/AddNew_Items";
import Edit_Items from "./components/Edit_Items";
import Add_Review from "./components/Add_Review";
import Log_in from "./components/Log_in";

export default {
  name: "App",
  components: {
    About_us,
    All_items,
    Add_Review,
    Contact_us,
    AddNew_Items,
    Edit_Items,
    Log_in,
  },
  data: function () {
    return {
      currentPage: "allitems",
    };
  },
  methods: {
    goaboutus: function () {
      this.currentPage = "aboutus";
    },
    goallitems: function () {
      this.currentPage = "allitems";
    },
    gologin: function () {
      this.currentPage = "login";
    },
    gocontactus: function () {
      this.currentPage = "contactus";
    },
    gonewitems: function () {
      this.currentPage = "addnewitems";
    },
    goaddReview: function (itemId) {
      this.currentPage = "add-reviews";
      this.reviewadded = itemId;
    },
    goedititems: function (itemId) {
      this.currentPage = "edit-items";
      this.itembeingEdited = itemId;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Amaranth:ital@0;1&family=Courgette&family=Gothic+A1:wght@200&family=Libre+Baskerville:ital@1&family=Marck+Script&family=Nanum+Myeongjo&family=Oleo+Script&family=Satisfy&family=Tangerine:wght@700&display=swap");
#maindiv {
  background-color: #f5f5f5;
  background-image: url("https://res.cloudinary.com/dfei0kzb6/image/upload/v1677925443/bgimg_2_prrrp3.jpg");
  font-family: "Amaranth", sans-serif;
  font-size: 16px;
  line-height: 1.5;
  margin: 0;
  padding: 0;
}

.navbar {
  background-color: #E0968B;
  border-radius: 5px;
}

.navbar-brand {
  font-weight: bold;
  margin-left: 10px;
  border-radius: 20px;
}

.navbarlogo {
  border-radius: 10px;
}

.navbar-nav .nav-link {
  color: #3B5249;
  font-weight: bold;
  font-size: 15pt;
  padding: 0.5rem 1rem;
  text-transform: uppercase;
  transition: all 0.2s ease-in-out;
}

.navbar-nav .nav-link:hover {
  background-color: #adc0c5;
  border-radius: 15px;
}

.nav-link{
  /* text-align: center; */
}

.card {
  border-radius: 0px 20px 0px 20px;
}

main {
  margin: 1rem;
  padding: 1rem;
}
</style>
