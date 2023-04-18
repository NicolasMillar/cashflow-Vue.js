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
          <Action />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" />
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
      movements: [
        {
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 1000,
          time: new Date("04-05-2023"),
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 500,
          time: new Date("04-015-2023"),
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: -100,
          time: new Date("03-25-2023"),
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 1000,
          time: new Date("02-01-2023"),
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: 1000,
          time: new Date("02-01-2023"),
        },
      ],
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
      console.log(lastDays);
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);

        return lastMovements.reduce((suma, movements) => {
          return suma + movements;
        }, 0);
      });
    },
  },
};
</script>
