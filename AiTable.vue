<template>
<!--:header-cell-style 设置表头的样式-->
  <el-table :data="tableData"
            :border="border"
            :header-cell-style="{background:'#40616C',color:'white'}"
            :stripe='stripe'
            :height="height"
   >
    <template v-if="extend &&extend.length>0">
    <el-table-column  :type="item.type" v-for="(item) in extend" :key="item.type" :label="item.label" :align="item.align">
    </el-table-column>
    </template>
    <el-table-column
      v-for="(item, index) in columns.slice(0,columns.length-1)"
      :key="index"
      :prop="item.prop"
      :label="item.label"
      :align="item.align"
    >
      <template slot-scope="scope">
        <div v-if="item.solt">
          <slot :name="item.solt" :scope="scope"></slot>
        </div>
        <div v-else>
          {{ scope.row[item.prop] }}
        </div>
      </template>
    </el-table-column>
    <el-table-column :label='columns[columns.length-1].label' :align='columns[columns.length-1].align'>
      <template slot-scope="scope">
      <slot name='action' :scope="scope">
      </slot>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  name: "",
  props: {
    // 数据
    tableData: {
      type: Array,
      required: true,
    },
    // 表格配置项
    columns: {
      type: Array,
      required: true,
    },
    // 边框
    border: {
      type: Boolean,
      default: false,
    },
    // 表格高度
    height: {
      type: String
    },
    // 斑马纹
    stripe: {
      type: Boolean,
      default: false,
    },
    // 扩展项
    extend: {
      type: Array
    },
  },
  data() {
    return {};
  },
  components: {},
  methods: {
  },
  mounted() {
  },
  computed: {},
  watch: {},
};
</script>

<style lang='less' scoped>

</style>