<template>
  <!-- <v-parallax dark src="@/assets/banner2_crop.jpg" height="800"> -->
  <v-parallax dark :src="imgBanner" height="800">
    <v-row align="start" justify="center">
      <v-col class="text-center" cols="12" style="margin-top: 230px">
        <v-fade-transition :key="inf.siteName">
          <h1 class="display-1 font-weight-thin mb-4">{{inf.siteName}}</h1>
        </v-fade-transition>
        <v-fade-transition>
          <h4 class="subheading">{{inf.siteSlug}}</h4>
        </v-fade-transition>
      </v-col>
    </v-row>
  </v-parallax>
</template>


<script>
import { db } from "@/main.js";
export default {
  data: () => ({
    inf: "",
    ref: db.collection("siteSetting"),
    imgBanner: ""
  }),
  created() {
    this.ref.onSnapshot(snap => {
      snap.forEach(snapp => {
        this.inf = snapp.data();
        this.imgBanner = snapp.data().siteHeader.ori;
      });
    });
  }
};
</script>