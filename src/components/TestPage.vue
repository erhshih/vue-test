<template>
  <div class="template">
    <div class="wrap">
      <div class="block">
        <input
          v-model.number="input"
          placeholder="請輸入正整數"
          oninput="value=value.replace(/[^0-9]/g,'')"
          v-on:change="changeHandler"
        />
      </div>

      <div class="block">
        <div class="scroll-content">
          <select id="mySelect">
            <option value="是否質數" :label="label1"></option>
            <option value="是否費氏數列" :label="label2"></option>
          </select>
        </div>
      </div>

      <div class="block">
        {{ col3 }}
      </div>
    </div>

    <input
      type="text"
      placeholder="请输入名字"
      v-model="keyWord"
      class="input"
    />
    <div class="wrap2">
      <div class="name" v-for="index in filPersons" :key="index.id">
        {{ index }}
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "TestPage",
  data() {
    return {
      keyWord: "",
      input: "",
      label1: "是否質數",
      label2: "是否費氏數列",
      col3: "true",
      names: [],
    };
  },
  mounted() {
    let vm = this;
    axios
      .get("https://api.publicapis.org/categories")
      .then(function (response) {
        console.log(response);
        console.log(response.data.categories[0]);
        vm.names = JSON.parse(response.request.responseText).categories;
      })
      .catch(function (error) {
        console.log(error);
      });
  },
  methods: {
    changeHandler() {
      let mySelect = document.getElementById("mySelect").value;

      if (mySelect == this.label1) {
        if (isPrimeNum(this.input)) {
          this.col3 = "true";
        } else {
          this.col3 = "false";
        }
      }

      // if (mySelect == this.label2) {
      //   for (let i = 1; i <= this.input; i++) {
      //     if (this.input == fib(i)) {
      //       this.col3 = "true";
      //     } else {
      //       this.col3 = "false";
      //     }
      //   }
      // }

      function isPrimeNum(num) {
        for (var i = 2; i < num; i) {
          if (num % i == 0) {
            return false;
          }
        }
        return true;
      }

      // function fib(n) {
      //   const arr = [0, 1];
      //   for (let i = 2; i <= n; i++) {
      //     arr[i] = arr[i - 1] + arr[i - 2];
      //   }
      //   return arr[n];
      // }
    },
  },

  computed: {
    filPersons() {
      return this.names.filter((p) => {
        return p.toLowerCase().indexOf(this.keyWord.toLowerCase()) !== -1;
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.input {
  margin: 4em 0 1em 0;
}

.wrap2 {
  width: 100%;
  border: 3px solid rgb(0, 195, 255);
  display: flex;
  flex-wrap: wrap;
  .name {
    border: 1px solid rgb(179, 179, 179);
    height: 1.5em;
    padding: 0.2em;
  }
}
.wrap {
  border: 1px solid #000;
  display: flex;
  justify-content: center;
  width: 100%;
  margin: 0 auto;
  .block:nth-child(1) {
    width: 200px;
    height: 50vh;
    border: 1px solid #000;
  }
  .block:nth-child(2) {
    width: 100%;
    height: 50vh;
    border: 4px solid rgb(255, 0, 0);
    // min-width: 100px;
    overflow-x: auto;
    overflow-y: hidden;
    .scroll-content {
      width: 600px;
      height: 50vh;
      background-color: transparent;
    }
  }
  .block:nth-child(3) {
    width: 300px;
    height: 50vh;
    border: 1px solid #000;
  }
}
</style>
