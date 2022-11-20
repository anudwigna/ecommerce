<template>
  <div>
    <SfHeader
      logo="shopLogo"
      title="Happytreats"
      active-icon="account"
      @click:account="onAccountClick"
    >
      <template v-if="categories" #navigation>
        <SfHeaderNavigationItem
          v-for="category in categories"
          :key="`sf-header-navigation-item-${category.id}`"
          :link="`/${category.code}`"
          :label="category.name"
        />
      </template>
      <template #search>
        <p></p>
      </template>
    </SfHeader>
    <SfHero>
      <SfHeroItem
        title="Happytreats is my name."
        button-text="Learn more"
        image="images/dog_1.jpg"
      />
      <SfHeroItem
        title="The one store that makes me feel happy"
        button-text="Learn more"
        image="images/dog_2.jpg"
      />
      <SfHeroItem
        title="Colorful summer dresses are already in store"
        button-text="Learn more"
        image="images/dog_3.jpg"
      />
    </SfHero>
    <div class="sf-heading" style="margin-top: 2%">
      <h2 class="sf-heading__title h2">Latest Products</h2>
    </div>
    <v-container>
      <v-row>
        <v-col v-for="product in products.items" :key="product.id" cols="3">
          <SfProductCard
            :title="product.name"
            :image="product.assets[0].preview"
            :show-add-to-cart-button="true"
            :score-rating="4"
            :max-rating="5"
            :regular-price="500"
            :special-price="450"
          ></SfProductCard>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
          <SfCallToAction
            title="Opening Offers are in row."
            button-text="Check Out Offers"
            description="Receive special offers and gifts for our customers."
            background="#424242"
            image="images/doggy.jpeg"
          />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import {
  SfHero,
  SfCallToAction,
  SfProductCard,
  SfHeader,
} from '@storefront-ui/vue';
import { gql } from 'graphql-tag';

const ALL_ITEMS_QUERY = gql`
  query ALL_PRODUCTS_QUERY {
    products(options: { take: 4, sort: { id: DESC } }) {
      totalItems
      items {
        id
        name
        slug
        assets {
          name
          preview
        }
      }
    }
  }
`;

const ALL_CATEGORIES = gql`
  query ALL_CATEGORIES {
    facets(options: { filter: { name: { eq: "category" } } }) {
      items {
        name
        code
        values {
          name
          id
          code
        }
      }
    }
  }
`;

export default {
  name: 'IndexPage',
  components: {
    SfHero,
    SfCallToAction,
    SfProductCard,
    SfHeader,
  },
  data: function () {
    return {
      products: { items: [{ assets: [{ name: '' }] }] },
      categories: [],
    };
  },
  apollo: {
    products: {
      query: ALL_ITEMS_QUERY,
      prefetch: true,
    },
    // facets: {
    //   query: ALL_CATEGORIES,
    //   prefetch: true,
    // },
  },
  async mounted() {
    const vm = this;
    const result = await vm.$apollo.query({
      query: ALL_CATEGORIES,
    });
    vm.categories = result.data.facets.items[0].values.slice(0, 3);
  },
  methods: {
    onAccountClick: function () {
      // console.log('HELLI');
    },
  },
};
</script>
