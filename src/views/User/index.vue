<template xmlns:el-col="http://www.w3.org/1999/html">
  <div>
    <el-row :gutter="16">
      <el-col :span="20">
        <div class="label-wrap">
          <div class="wrap-content">
            <el-row :gutter="16">
              <el-col :span="2">
                <label
                  for=""
                  style="font-size: 16px;float: right;padding-top: 8px"
                  >关键字：</label
                >
              </el-col>
              <el-col :span="3">
                <SelectVue :config="data.configOption"></SelectVue>
              </el-col>
              <el-col :span="4">
                <el-input placeholder="请输入搜索的关键字"></el-input>
              </el-col>
              <el-col :span="14">
                <el-button type="danger">搜索</el-button>
              </el-col>
            </el-row>
          </div>
        </div>
      </el-col>
      <el-col :span="4">
        <el-button type="danger" class="pull-right"> 添加用户 </el-button>
      </el-col>
    </el-row>
    <div class="black-space-30"></div>
    <TableVue :config="data.configTable">
      <template v-slot:status="slotData">
        <el-switch
          v-model="slotData.data.name"
          active-color="#13ce66"
          inactive-color="#ff4949"
        >
        </el-switch>
      </template>
      <template v-slot:operation="slotData">
        <el-button type="danger" size="mini" @click="operation(slotData.data)"
          >删除</el-button
        >
        <el-button type="success" size="mini" @click="operation(slotData.data)"
          >编辑</el-button
        >
      </template>
    </TableVue>
  </div>
</template>

<script>
import { reactive } from "@vue/composition-api";
// selcet 组件
import SelectVue from "@/components/Select";
import TableVue from "@/components/Table";
export default {
  name: "userIndex",
  components: { SelectVue, TableVue },
  setup() {
    const data = reactive({
      configOption: {
        init: ["name", "phone"]
      },
      // table组件配置参数
      configTable: {
        // 多选框
        selection: true,
        // 翻页记录checkbox,
        recordCheckbox: true,
        // 表头
        tHead: [
          { label: "邮箱/用户名", filed: "email", width: 200 },
          { label: "真实姓名", filed: "name", width: 120 },
          { label: "手机号", filed: "phone" },
          { label: "地址", filed: "address" },
          { label: "角色", filed: "role", width: 180 },
          {
            label: "禁启用状态",
            filed: "status",
            columnType: "slot",
            slotName: "status"
          },
          {
            label: "操作",
            columnType: "slot",
            slotName: "operation"
          }
        ],
        // 请求接口URL
        requestUrl: "/news/getList/"
      }
    });
    const operation = params => {
      console.log(params);
    };
    return {
      data,
      operation
    };
  }
};
</script>

<style scoped lang="scss">
@import "../../styles/config";
.label-wrap {
  label {
    @include labelDom(left, 60, 40);
  }
}
</style>
