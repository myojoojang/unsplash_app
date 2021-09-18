<template>
  <div class="card">
    <div class="card-text" @click="linkToProfile">
      <span>{{ item.user.first_name }}</span>
    </div>
    <img :src="item.urls.regular" @click="linkToImgPage" />
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    item: { type: Object, default: null },
  },
  methods: {
    linkToImgPage() {
      const url = this.item.links.html;
      window.open(url, "_blank");
    },
    linkToProfile() {
      const url = this.item.user.links.html;
      window.open(url, "_blank");
    },
  },
};
</script>
