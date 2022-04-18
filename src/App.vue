<script lang="ts" setup>
import { ref } from "vue";

/**
 *  装饰器测试
 */
const testDecorator = (target: any, key: String, descriptor: any) => {
  const old = descriptor.value;
  descriptor.value = function(...args) {
     return old.apply(this, args) + "_decorator_tail";
  }
};

class A {
  prefix: String;
  constructor() {
    this.prefix = "AClass_prefix_";
  }
  @testDecorator
  test1(name: String): String {
    return this.prefix +  "[hello:" + name + "]";
  }

   test2(): String {
    return this.test1("测试");
  }
}

function test() {
  const result = new A().test2();
  console.log("result is ===> " + result);
}

const form = ref({
  value: [
    {
      name: "",
      value: "",
    },
    {
      name: "",
      value: "",
    },
  ],
});
</script>

<template>
  <el-button @click="test">测试</el-button>
  <el-form :model="form">
    <el-table :data="form.value">
      <el-table-column label="名称">
        <template v-slot="{ $index }">
          <el-form-item :prop="`value[${$index}].name`" required>
            <el-input v-model="form.value[$index].name"></el-input>
          </el-form-item>
        </template>
      </el-table-column>

      <el-table-column label="数值">
        <template v-slot="{ $index }">
          <el-form-item :prop="`value[${$index}].value`" required>
            <el-input v-model="form.value[$index].value"></el-input>
          </el-form-item>
        </template>
      </el-table-column>
    </el-table>
  </el-form>
  <div>
    {{ form }}
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
