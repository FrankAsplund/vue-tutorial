<script>
import Card from "../components/Card.vue";

export default {
  components: {
    Card,
  },
};
</script>

<template>
  <main>
    <h1>
      This is the site where you rate the tracks on Phoebe Bridgers sophomore
      album "Punisher"
    </h1>
    <Card title="DVD Menu" length="1:09" />
    <Card title="Garden Song" length="3:39" />
    <Card title="Kyoto" length="3:04" />
    <Card title="Punisher" length="3:09" />
    <Card title="Halloween" length="4:31" />
    <Card title="Chinese Satellite" length="3:36" />
    <Card title="Moon Song" length="4:37" />
    <Card title="Saviour Complex" length="4:01" />
    <Card title="ICU" length="3:10" />
    <Card title="Graceland Too" length="3:56" />
    <Card title="I Know The End" length="5:44" />
  </main>
</template>

<style scoped>
h1 {
  margin-bottom: 1rem;
}
</style>
