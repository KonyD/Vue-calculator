<template>
  <div
    class="p-3"
    style="max-width: 400px; margin: 50px auto; background: #234"
  >
    <!-- Calculator Result -->
    <div
      class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark"
    >
      {{ calculatorValue || 0 }}
    </div>

    <!-- Calculator Buttons -->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{
            'bg-vue-green': ['C', '*', '/', '-', '+', '%', '='].includes(n),
          }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "Calculator",
  data() {
    return {
      calculatorValue: "",
      calculatorElements: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: null,
      previousValue: "",
    };
  },
  methods: {
    action(n: any) {
      // Append number
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }

      // Clear value
      if (n === "C") {
        this.calculatorValue = "";
      }

      // Percentage of the value
      if (n === "%") {
        this.calculatorValue = this.calculatorValue * 100 + "";
      }

      // Get operator
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousValue = this.calculatorValue;
        this.calculatorValue = "";
      }

      // Calculate the result
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousValue + this.operator + this.calculatorValue
        );

        this.previousValue = "";
        this.operator = null;
      }
    },
  },
};
</script>

<style>
.bg-vue-dark {
  background: #31475e;
}
.hover-class:hover {
  color: pointer;
  background: #4c729b;
}
.bg-vue-green {
  background: #3fb984;
}
</style>
