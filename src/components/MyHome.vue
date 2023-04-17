<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="'Ahorro total'" :total-amount="1000000" :amount="1000" />
    </template>
    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>

<script>
import Layout from "./MyLayout.vue";
import Header from "./MyHeader.vue";
import Resume from "./Resume/ResumeIndex.vue";
import Movements from "./MyMovements.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
  },
};
</script>
