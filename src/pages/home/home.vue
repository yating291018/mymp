<!-- -->
<template>
 <view>
   <view class='toolbar' @tap="format">
    <view :class="formats.bold ? 'ql-active' : ''" class="iconfont icon-zitijiacu" data-name="bold"></view>
    <view :class="formats.italic ? 'ql-active' : ''" class="iconfont icon-zitixieti" data-name="italic"></view>
    <view :class="formats.strike ? 'ql-active' : ''" class="iconfont icon-zitishanchuxian" data-name="strike"></view>
    <view :class="formats.align === 'left' ? 'ql-active' : ''" class="iconfont icon-zuoduiqi" data-name="align"
      data-value="left"></view>
    <view :class="formats.align === 'center' ? 'ql-active' : ''" class="iconfont icon-juzhongduiqi" data-name="align"
      data-value="center"></view>
    <view :class="formats.align === 'right' ? 'ql-active' : ''" class="iconfont icon-youduiqi" data-name="align"
      data-value="right"></view>
    <view :class="formats.align === 'justify' ? 'ql-active' : ''" class="iconfont icon-zuoyouduiqi" data-name="align"
      data-value="justify"></view>
    <view :class="formats.fontFamily ? 'ql-active' : ''" class="iconfont icon-font" data-name="fontFamily" data-value="Pacifico"></view>
    <view :class="formats.fontSize === '24px' ? 'ql-active' : ''" class="iconfont icon-fontsize" data-name="fontSize"
      data-value="24px"></view>
    <view :class="formats.color === '#0000ff' ? 'ql-active' : ''" class="iconfont icon-text_color" data-name="color"
      data-value="#0000ff"></view>
    <view :class="formats.backgroundColor === '#00ff00' ? 'ql-active' : ''" class="iconfont icon-fontbgcolor"
      data-name="backgroundColor" data-value="#00ff00"></view>
    <view :class="formats.list === 'ordered' ? 'ql-active' : ''" class="iconfont icon-youxupailie" data-name="list"
      data-value="ordered"></view>
    <view :class="formats.list === 'bullet' ? 'ql-active' : ''" class="iconfont icon-wuxupailie" data-name="list"
      data-value="bullet"></view>
    <view class="iconfont icon-undo" @tap="undo"></view>
    <view class="iconfont icon-redo" @tap="redo"></view>

    <view class="iconfont icon-outdent" data-name="indent" data-value="-1"></view>
    <view class="iconfont icon-indent" data-name="indent" data-value="+1"></view>
    <view class="iconfont icon-fengexian" @tap="insertDivider"></view>
    <view class="iconfont icon-charutupian" @tap="insertImage"></view>
    <view :class="formats.header === 1 ? 'ql-active' : ''" class="iconfont icon-format-header-1" data-name="header"
      :data-value="1"></view>
    <view class="iconfont icon-shanchu" @tap="clear"></view>
    <view :class="formats.direction === 'rtl' ? 'ql-active' : ''" class="iconfont icon-direction-rtl" data-name="direction"
      data-value="rtl"></view>
  </view>
  <editor
    id="editor"
    class="ql-container-edit"
    placeholder="请输入"
    :read-only="false"
    @ready="onEditorReady">
  </editor>
  <button @tap="publish" type="primary" class="getResult">发布</button>
  <view class='ql-container'>
    <view class="ql-editor">
      <view v-html="messageHtml"></view>
    </view>
  </view>
 </view>
</template>

<script>
export default {
  data () {
    return {
      editorCtx: '',
      formats: {},
      messageHtml: ''
    }
  },
  onLoad() {
	},
  methods: {
    onEditorReady() {
      uni.createSelectorQuery().select('#editor').context((res) => {
        this.editorCtx = res.context
      }).exec()
    },
    format(e) {
      let {
        name,
        value
      } = e.target.dataset
      if (!name) return
      // console.log('format', name, value)
      this.editorCtx.format(name, value)
    },
    insertDivider() {
      this.editorCtx.insertDivider({
        success: function() {
          console.log('insert divider success')
        }
      })
    },
    clear() {
      this.editorCtx.clear({
        success: function(res) {
          console.log("clear success")
        }
      })
    },
    insertImage() {
      uni.chooseImage({
        count: 1,
        success: (res) => {
          this.editorCtx.insertImage({
            src: res.tempFilePaths[0],
            alt: '图像',
            success: function() {
              console.log('insert image success')
            }
          })
        }
      })
    },
    publish () {
      let self = this
      this.editorCtx.getContents({
        success (res) {
          console.log('res', res)
          self.messageHtml = res.html
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "./home.css";
	.wrapper {
		padding: 5px;
	}
	.iconfont {
		display: inline-block;
		padding: 8px 8px;
		width: 24px;
		height: 24px;
		cursor: pointer;
		font-size: 20px;
	}
	.toolbar {
		box-sizing: border-box;
		border-bottom: 0;
		font-family: 'Helvetica Neue', 'Helvetica', 'Arial', sans-serif;
	}
	.ql-container-edit {
		box-sizing: border-box;
		padding: 5px;
		width: 100%;
		min-height: 30vh;
		height: auto;
		background: #fff;
		margin: 10px auto;
		font-size: 16px;
    line-height: 1.5;
    border: 1px solid #ccc;
	}
	.ql-active {
		color: #06c;
  }
  .getResult {
    width: 90%;
    font-size: 14px;
  }
</style>
