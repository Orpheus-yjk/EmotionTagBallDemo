<template>
  <div>
    <div style="margin: 32px">
      <el-form :model="filterData" label-width="80px">
        <el-form-item prop="text" label="数据上限">
          <el-input v-model="filterData.upperLimit"></el-input>
        </el-form-item>
        <el-form-item prop="time" label="创建时间">
          <el-date-picker
            v-model="filterData.time"
            placeholder="请选择日期"
            format="yyyy/MM/dd"
            valueFormat="yyyy/MM/dd"
            clearable
            style="width: 100%"
          />
        </el-form-item>
        <el-form-item prop="text" label="曲关键词">
          <el-input v-model="filterData.text"></el-input>
        </el-form-item>
        <el-form-item prop="name" label="图片名称">
          <el-input v-model="filterData.name"></el-input>
        </el-form-item>
        <el-form-item prop="type" label="曲风大类">
          <el-select
            v-model="filterData.type_qvfengdalei"
            multiple
            filterable
            clearable
            collapse-tags
            collapse-tags-tooltip
            style="width: 100%"
          >
            <el-option label="情歌" :value="0" />
            <el-option label="古风" :value="1" />
            <el-option label="摇滚说唱" :value="2" />
            <el-option label="欧美" :value="3" />
            <el-option label="虚拟人" :value="4" />
          </el-select>
        </el-form-item>
        <el-form-item prop="type" label="男频女频">
          <el-select
            v-model="filterData.type_nanpinnvpin"
            multiple
            filterable
            clearable
            collapse-tags
            collapse-tags-tooltip
            style="width: 100%"
          >
            <el-option label="女频" :value="51" />
            <el-option label="男频" :value="52" />
            <el-option label="中性" :value="53" />
            <el-option label="女SOLO" :value="54" />
          </el-select>
        </el-form-item>

        <el-form-item prop="type" label="情感基调">
          <el-select
            v-model="filterData.type_nannvweimian"
            multiple
            filterable
            clearable
            collapse-tags
            collapse-tags-tooltip
            style="width: 100%"
          >
            <el-option label="男调情" :value="101" />
            <el-option label="男深情" :value="102" />
            <el-option label="男炽热" :value="103" />
            <el-option label="女深情" :value="104" />
            <el-option label="女炽热" :value="105" />
            <el-option label="小女生" :value="106" />
            <el-option label="大女主" :value="107" />
            <el-option label="独立单身" :value="108" />
            <el-option label="不明确" :value="109" />
          </el-select>
        </el-form-item>

        <el-form-item prop="type" label="高级情感">
          <el-select
            v-model="filterData.type_gaoji"
            multiple
            filterable
            clearable
            collapse-tags
            collapse-tags-tooltip
            style="width: 100%"
          >
            <el-option label="放纵" :value="201" />
            <el-option label="孤独感" :value="202" />
            <el-option label="低压" :value="203" />
            <el-option label="无助疑问" :value="204" />
            <el-option label="凌乱感" :value="205" />
            <el-option label="无奈" :value="206" />
            <el-option label="遗憾" :value="207" />
            <el-option label="消极emo" :value="208" />
            <el-option label="太痛了" :value="209" />
            <el-option label="哭泣" :value="210" />
            <el-option label="回忆今昔" :value="211" />
            <el-option label="沦陷" :value="212" />

            <el-option label="迷蒙感" :value="220" />
            <el-option label="静美" :value="221" />
            <el-option label="盼爱" :value="222" />
            <el-option label="思念" :value="223" />
            <el-option label="哲理感" :value="224" />
            <el-option label="审视抽离" :value="225" />
            <el-option label="想象" :value="226" />
            <el-option label="忠贞" :value="227" />
            <el-option label="释然" :value="228" />
            <el-option label="开启遇见" :value="229" />
            <el-option label="结束分手" :value="230" />
            <el-option label="乞求母性光辉" :value="231" />
            <el-option label="挽回技巧" :value="232" />

            <el-option label="浪漫" :value="245" />
            <el-option label="喜感" :value="246" />
            <el-option label="勇气" :value="247" />
            <el-option label="主观主动" :value="248" />
            <el-option label="鼓励" :value="249" />
            <el-option label="爱自己" :value="250" />
            <el-option label="乐观向上" :value="251" />
            <el-option label="憧憬美好" :value="252" />
            <el-option label="甜美" :value="253" />
            <el-option label="炽热" :value="254" />
          </el-select>
        </el-form-item>
      </el-form>
      <el-button type="primary" @click="handleFilter">筛选</el-button>
      <el-button type="success" @click="handleReset">重置</el-button>
    </div>
    <div
      class="tagBall"
      ref="tagBall"
      @mouseover.self.stop="mouseOver"
      @mouseleave.self.stop="mouseLeave"
    >
      <a
        v-for="(item, index) in tagData"
        :key="index"
        class="tag"
        :title="item.text"
        @click="handleClick(item)"
      >
        {{ item.text }}
      </a>
    </div>

    <el-dialog
      :visible.sync="editInfo.show"
      :close-on-click-modal="false"
      :close-on-press-escape="false"
      :destroy-on-close="true"
      :append-to-body="true"
      top="64px"
    >
      <template #default>
        <img :src="require(`../assets/${editInfo.curData.url}`)" />
        <!-- 音频 -->
        <figure v-if="editInfo.curData.musicName">
          <audio
            controls
            :src="require(`../assets/MP3/${editInfo.curData.musicName}.mp3`)"
            style="width: 100%"
          ></audio>
        </figure>
        <!-- 音频END -->

        <el-form :model="editInfo.curData" label-width="80px">
          <el-form-item prop="text" label="曲关键词">
            <el-input v-model="editInfo.curData.text"></el-input>
          </el-form-item>
          <el-form-item prop="name" label="图片名称">
            <el-input v-model="editInfo.curData.name"></el-input>
          </el-form-item>
          <el-form-item prop="time" label="创建时间">
            <el-date-picker
              v-model="editInfo.curData.time"
              placeholder="请选择日期"
              format="yyyy/MM/dd"
              valueFormat="yyyy/MM/dd"
              clearable
              style="width: 100%"
            />
          </el-form-item>

          <el-form-item prop="type" label="曲风大类">
            <el-select
              v-model="editInfo.curData.type_qvfengdalei"
              multiple
              filterable
              clearable
              collapse-tags
              collapse-tags-tooltip
              style="width: 100%"
            >
              <el-option label="情歌" :value="0" />
              <el-option label="古风" :value="1" />
              <el-option label="摇滚说唱" :value="2" />
            </el-select>
          </el-form-item>

          <el-form-item prop="type" label="男频女频">
            <el-select
              v-model="editInfo.curData.type_nanpinnvpin"
              multiple
              filterable
              clearable
              collapse-tags
              collapse-tags-tooltip
              style="width: 100%"
            >
              <el-option label="女频" :value="51" />
              <el-option label="男频" :value="52" />
              <el-option label="中性" :value="53" />
              <el-option label="女SOLO" :value="54" />
            </el-select>
          </el-form-item>

          <el-form-item prop="type" label="情感基调">
            <el-select
              v-model="editInfo.curData.type_nannvweimian"
              multiple
              filterable
              clearable
              collapse-tags
              collapse-tags-tooltip
              style="width: 100%"
            >
              <el-option label="男调情" :value="101" />
              <el-option label="男深情" :value="102" />
              <el-option label="男炽热" :value="103" />
              <el-option label="女深情" :value="104" />
              <el-option label="女炽热" :value="105" />
              <el-option label="小女生" :value="106" />
              <el-option label="大女主" :value="107" />
              <el-option label="独立单身" :value="108" />
              <el-option label="不明确" :value="109" />
            </el-select>
          </el-form-item>

          <el-form-item prop="type" label="高级情感">
            <el-select
              v-model="editInfo.curData.type_gaoji"
              multiple
              filterable
              clearable
              collapse-tags
              collapse-tags-tooltip
              style="width: 100%"
            >
              <el-option label="放纵" :value="201" />
              <el-option label="孤独感" :value="202" />
              <el-option label="低压" :value="203" />
              <el-option label="无助疑问" :value="204" />
              <el-option label="凌乱感" :value="205" />
              <el-option label="无奈" :value="206" />
              <el-option label="遗憾" :value="207" />
              <el-option label="消极emo" :value="208" />
              <el-option label="太痛了" :value="209" />
              <el-option label="哭泣" :value="210" />
              <el-option label="回忆今昔" :value="211" />
              <el-option label="沦陷" :value="212" />

              <el-option label="迷蒙感" :value="220" />
              <el-option label="静美" :value="221" />
              <el-option label="盼爱" :value="222" />
              <el-option label="思念" :value="223" />
              <el-option label="哲理感" :value="224" />
              <el-option label="审视抽离" :value="225" />
              <el-option label="想象" :value="226" />
              <el-option label="忠贞" :value="227" />
              <el-option label="释然" :value="228" />
              <el-option label="开启遇见" :value="229" />
              <el-option label="结束分手" :value="230" />
              <el-option label="乞求母性光辉" :value="231" />
              <el-option label="挽回技巧" :value="232" />

              <el-option label="浪漫" :value="245" />
              <el-option label="喜感" :value="246" />
              <el-option label="勇气" :value="247" />
              <el-option label="主观主动" :value="248" />
              <el-option label="鼓励" :value="249" />
              <el-option label="爱自己" :value="250" />
              <el-option label="乐观向上" :value="251" />
              <el-option label="憧憬美好" :value="252" />
              <el-option label="甜美" :value="253" />
              <el-option label="炽热" :value="254" />
            </el-select>
          </el-form-item>
        </el-form>
      </template>
      <template #footer>
        <el-button type="danger" @click="handleClose">取消</el-button>
        <el-button type="primary" @click="handleSubmit">确定</el-button>
      </template>
    </el-dialog>
  </div>
</template>

<script>
import data from "./@config/index";
export default {
  components: {},
  data() {
    return {
      tagEle: "",
      paper: "",
      RADIUS: 280, //控制球型大小 280
      fallLength: 500,
      tags: [],
      angleX: Math.PI / 500,
      angleY: Math.PI / 500,
      CX: "",
      CY: "",
      EX: "",
      EY: "",
      timing: null,
      /** 标签筛选 */
      filterData: {
        upperLimit: null,
        name: "",
        text: "",
        type_qvfengdalei: [],
        type_nanpinnvpin: [],
        type_nannvweimian: [],
        type_gaoji: [],
        time: "",
      },
      /** 标签展示数据 */
      tagData: data,
      editInfo: {
        show: false,
        curData: null,
      },
    };
  },
  props: {},
  computed: {
    maxum: {
      get: () => this.wordList.sort()[0].value,
    },
  },
  watch: {},
  created() {},
  mounted() {
    // #region 球型标签相关逻辑
    this.tagEle = this.$refs.tagBall.children;
    this.paper = this.$refs.tagBall;
    this.CX = this.paper.offsetWidth / 2;
    this.CY = this.paper.offsetHeight / 2;
    this.EX =
      this.paper.offsetLeft +
      document.body.scrollLeft +
      document.documentElement.scrollLeft;
    this.EY =
      this.paper.offsetTop +
      document.body.scrollTop +
      document.documentElement.scrollTop;
    this.init();
    this.animate();
    // #region
  },
  methods: {
    // #region 筛选逻辑
    handleFilter() {
      let _data = data;
      if (this.filterData.name)
        _data = _data.filter((v) => v.name.includes(this.filterData.name));
      if (this.filterData.text)
        _data = _data.filter((v) => v.text.includes(this.filterData.text));

      // #region 选择框单选|多选 兼容
      //曲风大类
      const qvfengdaleis = Array.isArray(this.filterData.type_qvfengdalei)
        ? this.filterData.type_qvfengdalei
        : [this.filterData.type_qvfengdalei];
      //男频女频
      const nanpinnvpins = Array.isArray(this.filterData.type_nanpinnvpin)
        ? this.filterData.type_nanpinnvpin
        : [this.filterData.type_nanpinnvpin];
      //男女位面
      const nannvweimians = Array.isArray(
        this.filterData.type_nannvweimian
      )
        ? this.filterData.type_nannvweimian
        : [this.filterData.type_nannvweimian];
      //高级情感
      const type_gaojis = Array.isArray(this.filterData.type_gaoji)
        ? this.filterData.type_gaoji
        : [this.filterData.type_gaoji];
      // #endregion

      //曲风大类
      if (qvfengdaleis.length) {
        _data = _data.filter((v) => {
          const tags = Array.isArray(v.type_qvfengdalei)
            ? v.type_qvfengdalei
            : [v.type_qvfengdalei];
          const flag = qvfengdaleis.some((val) => tags.includes(val));
          return flag;
        });
      }
      //男频女频
      if (nanpinnvpins.length) {
        _data = _data.filter((v) => {
          const tags = Array.isArray(v.type_nanpinnvpin)
            ? v.type_nanpinnvpin
            : [v.type_nanpinnvpin];
          const flag = nanpinnvpins.some((val) => tags.includes(val));
          return flag;
        });
      }
      //男女位面
      if (nannvweimians.length) {
        _data = _data.filter((v) => {
          const tags = Array.isArray(v.type_nannvweimian)
            ? v.type_nannvweimian
            : [v.type_nannvweimian];
          const flag = nannvweimians.some((val) => tags.includes(val));
          return flag;
        });
      }
      //高级情感
      if (type_gaojis.length) {
        _data = _data.filter((v) => {
          const tags = Array.isArray(v.type_gaoji)
            ? v.type_gaoji
            : [v.type_gaoji];
          const flag = type_gaojis.some((val) => tags.includes(val));
          return flag;
        });
      }
      if (this.filterData.time) {
        // 创建时间>= 筛选时间
        _data = _data.filter((v) => {
          return +new Date(v.time) >= +new Date(this.filterData.time);
        });
      }
      if (this.filterData.upperLimit) {
        if (this.filterData.upperLimit > data.length) {
          this.$message({
            message: `数据上限不得超过80条`,//`数据上限不得超过${data}条`
            type: "warning",
          });
          return;
        } else {
          if (_data.length && _data.length > this.filterData.upperLimit) {
            // copy筛选结果
            const dataCopy = _data;
            // 重置数据为空
            _data = [];
            // 生成随机数数组
            const randoms = this.getRandom(
              this.filterData.upperLimit,
              0,
              dataCopy.length
            );
            // 通过随机队列循环获取数据
            randoms.forEach((val) => {
              _data.push(dataCopy[val]);
            });
          }
        }
      }
      this.tagData = _data;
      this.$nextTick(() => {
        this.init();
      });
    },
    handleReset() {
      this.filterData = {
        upperLimit: 40,//null,
        name: "",
        text: "",
        type_qvfengdalei: [],
        type_nanpinnvpin: [],
        type_nannvweimian: [],
        type_gaoji: [],
        time: "",
      };
      this.handleFilter();
    },
    getRandom(count, min, max) {
      let result = [];
      for (let i = 0; i < count; i++) {
        result.push(Math.floor(Math.random() * (max - min + 1)) + min);
      }
      return result;
    },
    // #endregion

    // #region 弹窗逻辑
    handleClick(curData) {
      this.editInfo.curData = curData;
      this.editInfo.show = true;
    },
    handleSubmit() {
      const index = this.tagData.findIndex(
        (v) => v.url == this.editInfo.curData.url
      );
      this.tagData.splice(index, 1, this.editInfo.curData);
      this.editInfo.show = false;
    },
    handleClose() {
      this.editInfo.show = false;
    },
    // #endregion

    // #region 球型标签相关逻辑
    init() {
      for (var i = 0; i < this.tagEle.length; i++) {
        var k = (2 * (i + 1) - 1) / this.tagEle.length - 1;
        var a = Math.acos(k);
        var b = a * Math.sqrt(this.tagEle.length * Math.PI);
        var x = this.RADIUS * Math.sin(a) * Math.cos(b);
        var y = this.RADIUS * Math.sin(a) * Math.sin(b);
        var z = this.RADIUS * Math.cos(a);
        // var t = this.tag({ ele: this.tagEle[i], x, y, z });
        this.tagEle[i].style.color =
          "rgb(" +
          parseInt(Math.random() * 255) +
          "," +
          parseInt(Math.random() * 255) +
          "," +
          parseInt(Math.random() * 255) +
          ")";
        this.tags.push({ ele: this.tagEle[i], x, y, z });
      }
    },
    tag({ ele, x, y, z }) {
      var scale = this.fallLength / (this.fallLength - z);
      var alpha = (z + this.RADIUS) / (2 * this.RADIUS);
      ele.style.fontSize = 15 * scale + "px";
      ele.style.opacity = alpha + 0.5;
      ele.style.filter = "alpha(opacity = " + (alpha + 0.5) * 100 + ")";
      ele.style.zIndex = parseInt(scale * 100);
      ele.style.left = x + this.CX - ele.offsetWidth / 2 + "px";
      ele.style.top = y + this.CY - ele.offsetHeight / 2 + "px";
    },
    animate() {
      this.timing = setInterval(() => {
        this.rotateX();
        this.rotateY();
        this.tags.forEach((item) => {
          this.tag(item);
        });
      }, 10); //改动过 原来40
    },
    rotateX() {
      var cos = Math.cos(this.angleX);
      var sin = Math.sin(this.angleX);
      this.tags.forEach((item) => {
        var y1 = item.y * cos - item.z * sin;
        var z1 = item.z * cos + item.y * sin;
        item.y = y1;
        item.z = z1;
      });
    },
    rotateY() {
      var cos = Math.cos(this.angleY);
      var sin = Math.sin(this.angleY);
      this.tags.forEach((item) => {
        var x1 = item.x * cos - item.z * sin;
        var z1 = item.z * cos + item.x * sin;
        item.x = x1;
        item.z = z1;
      });
    },
    mouseOver(event) {
      var x = event.clientX - this.EX - this.CX;
      var y = event.clientY - this.EY - this.CY;
      // console.log(x, y);
      this.angleY = x * 0.0001;
      this.angleX = y * 0.0001;
      if (!this.timing) this.animate();
    },
    mouseLeave(event) {
      var x = event.clientX - this.EX - this.CX;
      var y = event.clientY - this.EY - this.CY;
      this.angleY = x * 0.0001;
      this.angleX = y * 0.0001;
    },
    cheMouseOver() {
      clearInterval(this.timing);
      this.timing = null;
    },
    // #endregion
  },
};
</script>
<style scoped>
.tagBall {
  width: 500px;
  height: 500px;
  margin: 120px auto;
  position: relative;
}

.tag {
  display: block;
  position: absolute;
  left: 0px;
  top: 0px;
  color: #000;
  text-decoration: none;
  font-size: 15px;
  font-family: "微软雅黑";
  font-weight: bold;

  width: 180px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.tag:hover {
  border: #000 solid 1px;
  cursor: pointer;
}
.el-form {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

img {
  width: 100%;
  height: 220px;
  -o-object-fit: contain;
  object-fit: contain;
  border-radius: 4px;
  margin: 12px auto;
}
</style>
