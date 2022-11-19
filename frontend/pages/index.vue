<template>
  <div>
    <SfHero>
      <SfHeroItem
        title="Colorful summer dresses are already in store"
        subtitle="Summer Collection 2019"
        button-text="Learn more"
        image="images/dog_1.jpg"
      />
      <SfHeroItem
        title="Colorful summer dresses are already in store"
        subtitle="Summer Collection 2019"
        button-text="Learn more"
        image="images/dog_2.jpg"
      />
      <SfHeroItem
        title="Colorful summer dresses are already in store"
        subtitle="Summer Collection 2019"
        button-text="Learn more"
        image="images/dog_3.jpg"
      />
    </SfHero>
    <p v-for="item in products.items" :key="item.id">{{ item.name }}</p>
  </div>
</template>

<script>
import { SfHero } from '@storefront-ui/vue';
import { gql } from 'graphql-tag';

const ALL_ITEMS_QUERY = gql`
  query ALL_PRODUCTS_QUERY {
    products {
      totalItems
      items {
        name
        id
      }
    }
  }
`;

export default {
  name: 'IndexPage',
  components: {
    SfHero,
  },
  data: function () {
    return {
      products: { items: [] },
    };
  },
  apollo: {
    products: {
      query: ALL_ITEMS_QUERY,
      prefetch: true,
    },
  },
};
</script>
