<script lang="ts" setup>
import { ref } from "vue";
const form = ref({
  value: [
    {
      name: "",
      value: ""
    },
    {
      name: "",
      value: ""
    }
  ],
});
</script>

<template>
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
