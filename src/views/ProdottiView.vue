<template>
  <div class="align-center justify-center"
    style="height: 500px; width: 100%; padding-left: 70px; padding-right: 70px; padding-top: 75px;">
    <v-data-iterator :items="prodotti" :items-per-page="itemsPerPage">
      <template v-slot:header="{ page, pageCount, prevPage, nextPage }">
        <h1 class="text-h4 font-weight-bold d-flex justify-space-between mb-4 align-center">
          <div class="text-truncate">
            Products
          </div>

          <div class="d-flex align-center">
            <v-btn class="me-8"  @click="onClickSeeAll" color="indigo-lighten-1">
              <span class="text-none">See all</span>
            </v-btn>

            <div class="d-inline-flex">
              <v-btn :disabled="page === 1" icon="mdi-arrow-left" size="small" variant="tonal" class="me-2" color="indigo-lighten-1"
                @click="prevPage"></v-btn>

              <v-btn :disabled="page === pageCount" icon="mdi-arrow-right" size="small" variant="tonal" color="indigo-lighten-1"
                @click="nextPage"></v-btn>
            </div>
          </div>
        </h1>
      </template>

      <template v-slot:default="{ items }">
        <v-row>
          <v-col v-for="(item, i) in items" :key="i" cols="12" sm="6" xl="3">
            <v-sheet border>
              <v-carousel hide-delimiters progress="primary">
          <v-carousel-item v-for="(image, index) in item.raw.images" :key="index" :src="image" cover></v-carousel-item>
        </v-carousel>

              <v-list-item :title="item.raw.title" lines="two" density="comfortable" :subtitle=item.raw.description>
                <template v-slot:title>
                  <strong class="text-h6">
                    {{ item.raw.title }}
                  </strong>
                </template>
              </v-list-item>

              <v-table density="compact" class="text-caption">
                <tbody>
                  <tr align="right">
                    <th>Price:</th>
                    <td>{{ item.raw.price }}$</td>
                  </tr>
                  <tr align="right">
                    <th>Stock:</th>
                    <td>{{ item.raw.stock }}</td>
                  </tr>
                  <tr align="right">
                    <th>Category:</th>
                    <td>{{ item.raw.category }}</td>
                  </tr>
                  <tr align="right">
                    <th>Rating:</th>
                    <td><v-rating
          :model-value="item.raw.rating"
          color="amber"
          density="compact"
          half-increments
          readonly
          size="small"
        ></v-rating></td>
                  </tr>
                </tbody>
              </v-table>
            </v-sheet>
          </v-col>
        </v-row>
      </template>

      <template v-slot:footer="{ page, pageCount }">
        <v-footer color="indigo-lighten-1" class="justify-space-between text-body-2 mt-4">
          Total products: {{ prodotti.length }}

          <div>
            Page {{ page }} of {{ pageCount }}
          </div>
        </v-footer>
      </template>
    </v-data-iterator>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      prodotti: [],
      itemsPerPage: 4,
    };
  },
  mounted() {
    fetch('https://dummyjson.com/products')
      .then(res => res.json())
      .then(data => {
        this.prodotti = data.products;
      })
      .catch(error => {
        console.error('Error fetching products:', error);
      });
  },
  methods: {
    onClickSeeAll() {
      // Handle click on "See all" button if needed
    },
  },
};
</script>
  