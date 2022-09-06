<template>
  <div class="home">
    <div class="p-3 calMostParent">
      <div class="w-ful rounded m-1 p-3 text-end font-weight-bold text-white bgDark">
        {{ calValue || 0 }}
      </div>
      <div class="row no-gutters">
        <div class="col-3" v-for="item in calcuElements" :key="item">
          <div
            class="lead text-white text-center bgDark m-1 py-3 rounded elementHover"
            :class="{ 'actionBg': ['C', '*', '/', '-', '+', '%','=' ].includes(item)}" @click="elementAction(item)"
          >
            {{ item }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      calValue: "",
      previousCalValue:"",
      optr: null,
      calcuElements: [
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
    };
  },
  components: {},
  methods: {
    elementAction(e) {
      if(!isNaN(e) || e === '.' ){
        this.calValue += e + '';
      }

      if (e === 'C') {
        this.calValue = '';
      }

      if (e === '%') {
        this.calValue = this.calValue/100 + '';
      }
       if (['/','*','-','+'].includes(e)) {
        this.optr = e;
        this.previousCalValue = this.calValue;
        this.calValue ="";
       }
       if (e === "=") {
        this.calValue = eval(
          this.previousCalValue + this.optr + this.calValue
        );
        this.previousCalValue ="";
        this.optr =null;
       }
    }
  },
};
</script>

<style lang="scss">

.calMostParent {
  max-width: 400px;
  margin: 50px auto;
  background-color: #234;

  .bgDark {
    background-color: #31475e;
  }

  .elementHover {
    &:hover {
      cursor: pointer;
      background-color: #3d5875;
    }
  }

  .actionBg {
    background-color: #3fb984;
  }
}
</style>
