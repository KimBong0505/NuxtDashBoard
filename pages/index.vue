<script setup lang="ts">
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";

const list = [
  {
    title: "Today",
    component: resolveComponent("TabsToday"),
  },
  {
    title: "Week",
  },
  {
    title: "Month",
  },
  {
    title: "Year",
  },
];

let data = ref([
  16.0, 18.2, 23.1, 27.9, 32.2, 36.4, 39.8, 38.4, 35.5, 29.2, 22.0, 17.8,
]);

let categories = ref({
  today: [],
  week: [],
  month: [],
  year: [],
});

let currentCategories = ref("today");

const options = computed(() => ({
  chart: {
    type: "line",
    animation: {
      enabled: false,
    },
  },
  legend: {
    enabled: false,
  },
  title: {
    text: "Monthly Average Temperature",
  },

  xAxis: {
    gridLineColor: "transparent",
    categories: currentCategories,
  },
  yAxis: {
    gridLineColor: "transparent",
    title: {
      text: "Temperature (°C)",
    },
  },
  plotOptions: {
    line: {
      marker: {
        enabled: false,
      },
      dataLabels: {
        enabled: false,
      },
      enableMouseTracking: true,
    },
  },
  series: [
    {
      //data
      name: "line",
      lineWidth: "4px",
      color: {
        linearGradient: {},
        stops: [
          [0, "rgba(252,176,69,1)"],
          [0.33, "rgba(253,29,29,1)"],
          [0.66, "rgba(131,58,180,1)"],
          [1, "rgba(29,217,83,1)"],
        ],
      },
      data: data.value,
    },
  ],
}));

const setCategory = (e) => {
  let v = e.targer.innerText.toLowerCase();
  currentCategories.value = v;
};

function generateRandomData(number = 7) {
  let values = [];
  for (let i = 0; i < number + 1; i++) {
    values.push(Math.floor(Math.random() * 100));
  }

  console.log(values);
  data.value = values;
  return values;
}

onMounted(() => {
  generateRandomData();
});
</script>

<template>
  <div class="grid w-full gap-4">
    <header class="flex items-start justify-between">
      <div class="grow">
        <p>Hi, Welcome back Bong!</p>
        <h1>Dashboard</h1>
      </div>
      <div class="w-[120px] h-[36px] bg-neutral-200"></div>
    </header>
    <main class="grid gap-2">
      <template>
        <Tabs default-value="today" @click="setCategory">
          <TabsList class="max-w-[400px]">
            <TabsTrigger
              v-for="(item, index) in list"
              :key="index"
              :value="item.title"
            >
              {{ item.title }}
            </TabsTrigger>
          </TabsList>
          <TabsContent
            v-for="(item, index) in list"
            :key="index"
            :value="item.title"
          >
            <!-- {{ item.component }} -->
            <highchart :options="options" />
          </TabsContent>
        </Tabs>
      </template>
      <!-- <div class="flex items-center gap-4">
        <div
          v-for="(item, index) in 3"
          :key="index"
          class="w-[120px] h-[36px] bg-neutral-200"
        ></div>
      </div>
      <section>
        <div class="w-full h-[360px] bg-neutral-200"></div>
      </section> -->
    </main>
    <footer>
      <div class="flex items-center gap-4">
        <div
          v-for="(item, index) in 3"
          :key="index"
          class="w-full h-[260px] bg-neutral-200"
        ></div>
      </div>
    </footer>
  </div>
</template>

<style scoped></style>
