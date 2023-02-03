<template>
  <div id="wrap">
    <div id="container">
      <h1 id="title">신상품</h1>
      <h3 id="subtitle">새로운 상품을 만나 보세요</h3>
      <div id="lists">
        <div
          class="product"
          v-for="one in products"
          :key="one.name"
          :style="{ width: `calc(100% /${column} - (10px)` }"
        >
          <img :src="`${one.imgurl}`" :alt="`${one.name}`" />
          <div class="info">
            <h5 :style="{ color: brand.color, fontSize: brand.size }">
              {{ one.brand }}
            </h5>
            <h4
              :style="{ color: productname.color, fontSize: productname.size }"
            >
              {{ one.name }}
            </h4>
            <h5 :style="{ color: explain.color, fontSize: explain.size }">
              {{ one.subtitle }}
            </h5>
            <div class="price">
              <div
                class="final"
                :style="{ color: finalprice.color, fontSize: finalprice.size }"
              >
                {{ one.finalprice | comma }}원
              </div>
              <div
                class="saleAmount"
                :style="{ color: saleamount.color, fontSize: saleamount.size }"
              >
                - {{ (one.originalprice - one.finalprice) | comma }}원
              </div>
            </div>
            <div
              class="origin"
              :style="{
                color: originalprice.color,
                fontSize: originalprice.size,
              }"
            >
              {{ one.originalprice | comma }}원
            </div>
          </div>
        </div>
      </div>
    </div>
    <div id="setting">
      <div class="row">
        <div class="subject">컬럼수</div>
        <div class="object">
          <div></div>
          <input
            name="column"
            type="text"
            placeholder="최대 6까지"
            v-on:input="columninput"
          />
        </div>
      </div>
      <div class="row" v-for="one in setting" :key="one.name">
        <div class="subject">{{ one.subject }}</div>
        <div class="object">
          <div>글씨색상</div>
          <input
            :name="one.name"
            class="color"
            type="text"
            placeholder="컬러명 혹은 헥스코드"
            v-on:input="otherinput"
          />
        </div>
        <div class="object">
          <div>글씨크기</div>
          <input
            :name="one.name"
            class="size"
            type="text"
            placeholder="px 단위와 함께 작성"
            v-on:input="otherinput"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const productsData = [
  {
    brand: "샘표",
    imgurl:
      "https://img.danawa.com/prod_img/500000/028/731/img/8731028_1.jpg?shrink=330:330&_v=20190718174847",
    name: "진간장 금S 1.8L",
    subtitle: "언제나 함께해 온 그 맛",
    originalprice: "9000",
    finalprice: "1000",
  },
  {
    brand: "동서식품",
    imgurl:
      "https://img.danawa.com/prod_img/500000/167/251/img/2251167_1.jpg?shrink=330:330&_v=20211220165049",
    name: "[맥심] 모카골드 250T",
    subtitle: "커피 한 잔의 여유",
    originalprice: "31500",
    finalprice: "27900",
  },
  {
    brand: "동원",
    imgurl:
      "https://img.danawa.com/prod_img/500000/474/457/img/13457474_1.jpg?shrink=330:330&_v=20220303133248",
    name: "딤섬 부추 창펀 390g x 2개입",
    subtitle: "소스와 함께먹는 부드러운",
    originalprice: "8980",
    finalprice: "6980",
  },
  {
    brand: "동원",
    imgurl:
      "https://img.danawa.com/prod_img/500000/442/987/img/16987442_1.jpg?shrink=330:330&_v=20220504161541",
    name: "딤섬 샤오롱바오 390g x 2개입",
    subtitle: "고소한 육즙 가득",
    originalprice: "8980",
    finalprice: "6980 ",
  },
];

const settingData = [
  { subject: "브랜드명", name: "brand" },
  { subject: "상품명", name: "productname" },
  { subject: "설명", name: "explain" },
  { subject: "판매금액", name: "finalprice" },
  { subject: "할인금액", name: "saleamount" },
  { subject: "원가", name: "originalprice" },
];

export default {
  created() {},
  filters: {
    comma(val) {
      return String(val).replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      //return val.toLocaleString("ko-KR");
    },
  },
  data() {
    return {
      column: 4,
      brand: {
        color: "gray",
        size: "13px",
      },
      productname: {
        color: "black",
        size: "16px",
      },
      explain: {
        color: "gray",
        size: "12px",
      },
      finalprice: {
        color: "black",
        size: "18px",
      },
      saleamount: {
        color: "red",
        size: "16px",
      },
      originalprice: {
        color: "gray",
        size: "16px",
      },
      setting: settingData,
      products: productsData,
    };
  },
  methods: {
    columninput: function (e) {
      this.column = e.target.value;
    },
    otherinput: function (e) {
      this[e.target.name][e.target.className] = e.target.value;
    },
  },
};
</script>

<style scoped>
#wrap {
  display: flex;
  min-width: 1080px;
}

#container {
  width: 80%;
  height: auto;
  text-align: center;
}

#title {
  margin: 50px 0 10px;
}

#subtitle {
  color: gray;
  margin: 0 0 100px 0;
}

#lists {
  display: flex;
  /* gap: 10px; */
  flex-wrap: wrap;
  justify-content: space-between;
  width: 100%;
}

.product {
  /* width: 200px; */
  min-width: calc(100% / 6);
  margin-bottom: 20px;
}

.product img {
  width: 100%;
  height: auto;
  overflow: hidden;
  border: 1px solid lightgray;
  box-sizing: border-box;
}

.info {
  text-align: left;
  margin: 10px 0 10px 10px;
}

.info h4 {
  margin: 5px 0;
}

.info h5 {
  color: gray;
  margin: 0;
}

.price {
  display: flex;
  margin: 5px 0;
  font-weight: bold;
}

.price .final {
  font-size: 18px;
  margin-right: 10px;
}

.price .saleAmount {
  color: red;
}

.origin {
  text-decoration: line-through;
  color: gray;
}

#setting {
  width: calc(20% - 10px);
  margin-left: 10px;
  background-color: lightgray;
  padding-left: 10px;
}

.row {
  margin: 20px 0;
}

.row:first-child {
  display: flex;
}

.subject {
  font-weight: bold;
  margin-bottom: 10px;
}

.object {
  display: flex;
  margin-bottom: 10px;
}

.object div {
  margin-right: 10px;
}
</style>
