<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume
        :label="label"
        :date="totalAmount"
        :total-amount="1000000"
        :amount="amount"
      >
        <template #graphic>
          <Graphic :amounts="amounts" />
        </template>
        <template #action>
          <Action @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove" />
    </template>
  </Layout>
</template>

<script>
import Layout from "./MyLayout.vue";
import Header from "./MyHeader.vue";
import Resume from "./Resume/ResumeIndex.vue";
import Movements from "./Movements/MyMovements.vue";
import Action from "./MyAction.vue";
import Graphic from "./Resume/MyGraphic.vue";

export default {
  components: {
    Layout,
    Header,
    Resume,
    Movements,
    Action,
    Graphic,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const olDate = today.setDate(today.getDate() - 30);

          return m.time >= olDate;
        })
        .map((m) => m.amount);
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);

        return lastMovements.reduce((suma, movements) => {
          return suma + movements;
        }, 0);
      });
    },
  },
  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));

    if (Array.isArray(movements)) {
      this.movements = movements.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },
  methods: {
    create(movements) {
      this.movements.push(movements);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
  },
};
</script>
