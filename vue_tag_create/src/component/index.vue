<template>
    <div>
        <div class="input-tag-wrapper">
            <span
                class="input-tag"
                v-for="(item, index) in tagArray"
                :key="index"
            >
                {{ item }}
                <a class="remove" @click="removeTag(index)"
                ><i class="iconfont icon-close"></i
                ></a>
            </span>
            <input
                placeholder="输入文字敲回车生成标签，总字数不超过15个"
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
            <p v-show="showCheckChar">
                <i class="iconfont icon-warn"></i>
        标签不能包含空格或特殊字符
            </p>
            <p v-show="showCheckLength"><i class="iconfont icon-warn"></i>
            已超15个字
            </p>
        </div>
    </div>
</template>

<script>
export default {
  name: "ContentEditor",
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
      return this.tagTotalLengh <= 15;
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
      }
    },

    // 删除标签
    removeTag(index) {
      this.tagArray.splice(index, 1);
    }
  }
};
</script>

<style lang="scss">
.input-tag-wrapper {
    width: 51rem;
    border-radius: 4px;
    border: 1px solid #dcdfe6;
    color: #606266;
    height: 3.2rem;
    line-height: 3.2rem;
    padding: 0 .5rem;
    display: flex;
    align-items: center;
    .new-tag {
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
    .input-tag {
      background-color: #f6f6f6;
      border-color: #e9e9eb;
      color: #909399;
      height: 2rem;
      line-height: 2rem;
      font-size: 1.2rem;
      padding: 0.3rem 0.5rem;
      border-radius: 0.3rem;
      margin-right: 0.4rem;
      .remove {
        cursor: pointer;
      }
      i{
        font-size: 10px;
      }
    }
  }
</style>