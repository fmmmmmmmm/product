<template>
  <div>
    <div class="product">
      <p>商品id:{{ currentProduct.id }}</p>
      <p>商品名字:{{ currentProduct.name }}</p>
      <p>商品价格:{{ currentProduct.price }}</p>
      <p>商品图片:<img :src="currentProduct.img" /></p>
      <p>商品库存:{{ currentProduct.num }}</p>
    </div>
    <div class="commentlist">
      <ul>
        <li v-for="item in currentProduct.comments" :key="item.content">
          {{ item.name }} ----> {{ item.content }}
        </li>
      </ul>
    </div>
    <div class="commentbox">
      <Cmtbox @func="receiveFromChild"></Cmtbox>
    </div>
  </div>
</template>

<script>
import Cmtbox from "./Cmtbox.vue";
export default {
  data() {
    return {
      id: this.$route.params.id,
      products: this.products,
    };
  },
  computed: {
    currentProduct() {
      return this.products.find((item) => {
        if (item.id == this.id) {
          return item;
        }
      });
    },
  },
  components: {
    Cmtbox,
  },
  methods: {
    receiveFromChild(obj) {
      this.currentProduct.comments.push(obj);
    },
  },
};
</script>

<style lang="less">
.product,
.commentlist,
.commentbox {
  padding: 10px;
  width: 500px;
  margin: 30px auto;
  border: 1px solid pink;
  img {
    width: 80%;
  }
}
</style>