<template>
  <div>
    <el-form :inline="true" class="demo-form-inline">
      <el-row :gutter="20">
        <el-col :span="4">
          <div class="label-wrap">
            <label for="">类型：</label>
            <div class="warp-content">
              <el-select
                v-model="value"
                placeholder="请选择"
                style="width: 100%"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                >
                </el-option>
              </el-select>
            </div>
          </div>
        </el-col>
        <el-col :span="8">
          <!--          <div class="label-wrap">-->
          <!--            <label for="">日期：</label>-->
          <!--            <div class="warp-content">-->
          <!--            <el-date-picker-->
          <!--              v-model="value2"-->
          <!--              type="datetimerange"-->
          <!--              align="right"-->
          <!--              start-placeholder="开始日期"-->
          <!--              end-placeholder="结束日期"-->
          <!--              :default-time="['12:00:00', '08:00:00']"-->
          <!--            >-->
          <!--            </el-date-picker>-->
          <!--            </div>-->
          <!--          </div>-->

          <el-form-item label="日期：">
            <el-date-picker
              v-model="value2"
              type="datetimerange"
              align="right"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
              :default-time="['12:00:00', '08:00:00']"
            >
            </el-date-picker>
          </el-form-item>
        </el-col>
        <el-col :span="3">
          <el-form-item label="关键字：">
            <el-select v-model="search_key" style="width: 80px">
              <el-option
                v-for="item in searchOption"
                :key="item.value"
                :value="item.value"
                :label="item.label"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="4">
          <el-input
            v-model="search_keyWork"
            placeholder="请输入内容"
          ></el-input>
        </el-col>
        <el-col :span="3">
          <el-button type="danger">搜索</el-button>
        </el-col>
        <el-col :span="2">
          <el-button type="danger">新增</el-button>
        </el-col>
      </el-row>
    </el-form>
  </div>
</template>

<script>
import { reactive, ref } from "@vue/composition-api";

export default {
  name: "infoIndex",
  setup() {
    const options = reactive([
      {
        value: "选项1",
        label: "国际信息"
      },
      {
        value: "选项2",
        label: "国内信息"
      },
      {
        value: "选项3",
        label: "行业信息"
      }
    ]);
    // 搜索关键字
    const searchOption = reactive([
      { value: "id", label: "ID" },
      { value: "title", label: "标题" }
    ]);
    const search_key = ref("title");
    const value = ref("");
    const value2 = ref("");
    const search_keyWork = ref("");
    return {
      options,
      value,
      value2,
      searchOption,
      search_key,
      search_keyWork
    };
  }
};
</script>

<style lang="scss" scoped>
// label-wrap 下面含有warp-content，效果时自动适应宽度，左对齐
.label-wrap {
  label {
    float: left;
    line-height: 40px;
    width: 60px;
  }
  .warp-content {
    margin-left: 80px;
  }
}
</style>
