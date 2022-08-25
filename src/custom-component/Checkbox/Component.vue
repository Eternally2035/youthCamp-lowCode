<template>
    <div class="checkbox">
      <el-checkbox class="checkbox-demo" v-model="checkList">
        <el-checkbox label="未命名1"></el-checkbox>
        <el-checkbox label="未命名2"></el-checkbox>
        <el-checkbox label="未命名3"></el-checkbox>
      </el-checkbox>
      <el-radio-group class="checkbox-radio-demo" v-model="radio">
        <el-radio :label="未命名1"></el-radio>
        <el-radio :label="未命名2"></el-radio>
        <el-radio :label="未命名3"></el-radio>
      </el-radio-group>
    </div>
</template>

<script>
import OnEvent from "../common/OnEvent";

export default {
  extends: OnEvent,
  props: {
    propValue: {
        type: String,
        required: true,
        default: "",
    },
    element: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style>
.line-shape {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  overflow: auto;
}
</style>