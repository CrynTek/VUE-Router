<template>
  <div>
    <div style="background-color: #FFBC80">
      <v-container>
        <center>
          <h1
            class="
            text-center
            transition-swing
            v-btn
            v-btn--top
            v-btn--is-elevated
            v-btn--fab
            v-btn--fixed
            v-btn--has-bg
            v-btn--right
            v-size--large
            black
            mt-10
          "
            style="
              color: white;
              text-align: center;
              font-size: large;
              width: 100%;
              
            "
          >
            Product
          </h1>
        </center>
        <v-container class="d-flex flex-wrap">
          <v-card
            class="mx-auto mb-5"
            max-width="400"
            style="color: #004d40"
            v-for="(i, index) in productlist"
            :key="index"
          >
            <v-img height="450px" :src="i.image"> </v-img>
            <v-card-title class="font-weight-h1">{{ i.name }}</v-card-title>

            <v-card-subtitle class="pb-0">{{ i.rightText }}</v-card-subtitle>

            <v-card-text class="text--primary">
              <div style="font-size: large">{{ i.leftText }}</div>
              <!-- <p class="text-h6 text--primary">{{ i.rightText }}</p> -->
            </v-card-text>

            <div class="d-flex justify-space-around mb-6">
              <v-sheet
                color="#9BB7D4"
                elevation="6"
                height="51"
                outlined
                shaped
                width="380px"
                class="d-flex justify-space-around mb-3 align-center"
              >
                <v-btn color="black" text :to="'/detail/' + i.rightText"
                  >detail</v-btn
                >
                <v-btn color="orange" @click="selected(index)"> Add </v-btn>
                <v-btn color="orange"> {{ i.amount }} </v-btn>
              </v-sheet>
            </div>
          </v-card>
        </v-container>
        <div
          class="
            text-center
            transition-swing
            v-btn
            v-btn--bottom
            v-btn--is-elevated
            v-btn--fab
            v-btn--fixed
            v-btn--has-bg
            v-btn--right
            v-size--large
            black
          "
        >
          <v-bottom-sheet v-model="sheet" inset>
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="orange" v-bind="attrs" v-on="on"> Cart</v-btn>
            </template>
            <v-sheet class="text-center" height="200px">
              <v-btn class="mt-6" text color="error" @click="sheet = !sheet">
                close
              </v-btn>
              <div class="my-3">
                <h4 class="text-center">Total {{ total() }} Baht</h4>
              </div>
            </v-sheet>
          </v-bottom-sheet>
        </div>
        <div
          class="
            text-center
            transition-swing
            v-btn
            v-btn--bottom
            v-btn--is-elevated
            v-btn--fab
            v-btn--fixed
            v-btn--has-bg
            v-btn--right
            v-size--large
            mb-15
            black
          "
        >
          <v-bottom-sheet v-model="detailsheet" inset>
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="orange" v-bind="attrs" v-on="on"> detail</v-btn>
            </template>
            <v-sheet class="text-center" height="200px">
              <v-btn class="mt-6" text color="error" @click="detailsheet = !detailsheet">
                close
              </v-btn>
              <div class="my-3">
                 <v-container grid-list-xs class="white">
          <router-view :key="$route.path"></router-view>
        </v-container>
              </div>
            </v-sheet>
          </v-bottom-sheet>
        </div>
        
        <!-- <v-container grid-list-xs class="white">
          <router-view :key="$route.path"></router-view>
        </v-container> -->
      </v-container>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      detailsheet: false,
      sheet: false,
      productlist: [
        {
          id: "#001",
          name: "มาม่ารสหมูสับ (ถ้วย)",
          image: "https://media.shopat24.com/pdmain/363003_00_grocery.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสหมูสับ ตรามาม่า",
          leftText: "Price : 15",
          amount: 0,
          price: 15,
          reveal: false,
        },
        {
          id: "#002",
          name: "มาม่ารสต้มยำกุ้ง (ถ้วย)",
          image: "https://media.shopat24.com/pdmain/120182_010_04.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสต้มยำกุ้ง ตรามาม่า",
          leftText: "Price : 15",
          amount: 0,
          price: 15,
          reveal: false,
        },
        {
          id: "#003",
          name: "มาม่ารสต้มยำกุ้งน้ำข้น (ถ้วย)",
          image:
            "https://media.allonline.7eleven.co.th/pdmain/393905_010_Supermarket.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสต้มยำกุ้งข้ำข้น ตรามาม่า",
          leftText: "Price : 15",
          amount: 0,
          price: 15,
          reveal: false,
        },
        {
          id: "#004",
          name: "มาม่ารสผัดไข่เค็ม (ถ้วย)",
          image:
            "https://backend.tops.co.th/media/catalog/product/8/8/8850987148767.jpg",
          rightText:
            "บะหมี่ถ้วยกึ่งสำเร็จรูปออเรียนทัลคิตเชน รสผัดไข่เค็ม ตรามาม่า",
          leftText: "Price : 15",
          amount: 0,
          price: 15,
          reveal: false,
        },
        {
          id: "#005",
          name: "มาม่ารสหมูสับ ",
          image:
            "https://th-test-11.slatic.net/p/c569b7c19c13c590282803443a22271f.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสหมูสับ ตรามาม่า",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#006",
          name: "มาม่ารสต้มยำกุ้ง ",
          image: "https://media.shopat24.com/pdmain/125330_01_Supermarkets.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสต้มยำกุ้ง ตรามาม่า",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#007",
          name: "มาม่ารสต้มยำกุ้งน้ำข้น ",
          image:
            "https://cf.shopee.co.th/file/300870436f6c85277f8b8efb24ca00f6",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสต้มยำกุ้งน้ำข้น ตรามาม่า",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#008",
          name: "ม่าม่า วุ้นเส้นน้ำใส ",
          image:
            "https://media.allonline.7eleven.co.th/pdmain/423832_00_instant-food_mama_v1.jpg",
          rightText: "วุ้นเส้นกึ่งสำเร็จรูปน้ำใส ตรามาม่า",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#009",
          name: "ไวไว รสหมูสับต้มยำ",
          image:
            "https://media.shopat24.com/pdmain/357111_02_Supermarket_Edit_1.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสหมูสับต้มยำ ตราไวไว",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#010",
          name: "ไวไว รสหมูสับ",
          image: "https://positioningmag.com/wp-content/uploads/2018/11/s.gif",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสหมูสับ ตราไวไว",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#011",
          name: "ยำยำ จัมโบ้ รสต้มยำกุ้งน้ำข้น",
          image:
            "https://secure.ap-tescoassets.com/assets/TH/391/8850250005391/ShotType1_540x540.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสต้มยำกุ้งน้ำข้น ตรายำยำ จัมโบ้",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
        {
          id: "#012",
          name: "ยำยำ จัมโบ้ รสหมูสับ",
          image:
            "https://media.shopat24.com/pdmain/125332_02_Supermarket_Edit_1.jpg",
          rightText: "บะหมี่กึ่งสำเร็จรูป รสหมูสับ ตรายำยำ จัมโบ้",
          leftText: "Price : 6",
          amount: 0,
          price: 6,
          reveal: false,
        },
      ],
    };
  },
  methods: {
    selected: function (index) {
      this.productlist[index].amount++;
    },
    total: function () {
      var sum = 0;
      this.productlist.forEach(function (i) {
        sum += i.amount * i.price;
      });
      return sum;
    },
  },
};
</script>

<style>
h2 {
  color: white;
}
</style>
