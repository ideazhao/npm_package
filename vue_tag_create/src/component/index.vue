<template>
    <div :class="inline?'layout-inline':''">
        <div class="input-tag-wrapper">
            <span
                class="input-tag"
                v-for="(item, index) in tagArray"
                :key="index"
            >
                {{ item }}
                <a class="remove" @click="removeTag(index)"
                ><i :class="iconClass"></i
                ></a>
            </span>
            <input
                :placeholder="placeholder"
                type="text"
                class="new-tag"
                v-model="inputTag"
                @input="checkChar"
                @keyup.enter="addTag"
                @blur="
                () => {
                    showCheckChar = false;
                    showCheckLength = false;
                }
                "
            />
        </div>
        <div class="error-tips">
            <span v-show="showCheckChar">
                <i class="iconfont icon-warn"></i>标签不能包含空格或特殊字符
            </span>
            <span v-show="showCheckLength"><i class="iconfont icon-warn"></i>
            已超{{limit}}个字
            </span>
        </div>
    </div>
</template>

<script>
export default {
  name: "TagInput",
  props: {
    'inline':{
      type:Boolean,
      default:false
    },
    'iconClass':{
      type:String,
      default:''
    },
    'limit':{
      type:String,
      default:'15'
    },
    "placeholder":{
      type:String,
      default:'输入文字，敲回车生成标签'
    },
  },
  data() {
    return {
        //编辑相关
        inputTag:"", //输入绑定值
        showCheckChar: false, //字符不合格提示
        showCheckLength: false, //字符过长提示
        tagTotalLengh: 0,

        // 用于显示标签的数组
        tagArray:[]

    };
  },
  methods: {
    // 检查特殊字符
    checkChar() {
      let reg = /^[\u4e00-\u9fa5_a-zA-Z0-9]+$/;
      return reg.test(this.inputTag);
    },

    // 检查长度,不能超过15
    checkLength() {
      this.tagTotalLengh = this.tagArray.join("").length + this.inputTag.length;
      return this.tagTotalLengh <= this.limit;
    },

    // 添加标签
    addTag() {
      //添加标签
      let charOk = this.checkChar(),
        lengthOk = this.checkLength();
      if (!charOk) {
        this.showCheckChar = true;
      }
      if (!lengthOk) {
        this.showCheckLength = true;
      }
      if (charOk && lengthOk) {
        this.showCheckChar = false;
        this.showCheckLength = false;
        this.tagArray.push(this.inputTag);
        this.inputTag = "";
        //添加的标签传给父组件
        this.$emit("addTag",this.tagArray)
      }
    },

    // 删除标签
    removeTag(index) {
      this.tagArray.splice(index, 1);
      //添加的标签传给父组件
      this.$emit("removeTag",this.tagArray)
    }
  }
};
</script>

<style scoped>

.input-tag-wrapper {
  min-width: 300px;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  color: #606266;
  height: 3.2rem;
  line-height: 3.2rem;
  padding: 0 .5rem;
  display: flex;
  align-items: center;
  overflow: auto;
}
.input-tag-wrapper .input-tag {
  background-color: #f6f7f9;
  color: #909399;
  height: 2rem;
  line-height: 2rem;
  font-size: 1.2rem;
  padding: 0.3rem 0.5rem;
  border-radius: 0.3rem;
  margin-right: 0.4rem;
}
.input-tag-wrapper .input-tag .remove {
  cursor: pointer;
}
.input-tag-wrapper .input-tag .remove i{
  font-size: 10px;
}
.input-tag-wrapper  .new-tag {
  background: transparent;
  border: 0;
  color: #777;
  font-size: 13px;
  font-weight: 400;
  outline: none;
  padding: 5px;
  -webkit-box-flex: 1;
  -ms-flex-positive: 1;
  flex-grow: 1;
}
.input-tag-wrapper .new-tag::-webkit-input-placeholder{
  color: #ccc;
}
.error-tips{
  margin-top: 5px;
  color: #fb3a3a;
  display: flex;
  align-items: center;
}

/* 设置行内布局 */
.layout-inline{
  display: flex;
  align-items: center;
}
.layout-inline .error-tips{
  margin-left: 10px;
}
</style>