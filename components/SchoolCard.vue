<template>
  <div class="school-card">
    <div class="data">
      <div class="action">
        <img
          v-if="schoolData.logo_url !== null"
          :src="schoolData.logo_url"
          alt=""
        />
        <img v-else src="/images/school-logo.png" alt="school logo" />
        <span>{{ schoolData.school_name }}</span>
      </div>
      <button>Join Campaign</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "SchoolCard",
  props: ["schoolData"],
};
</script>
<style scoped>
.school-card {
  background-color: #f9f9f9;
  padding: 10px 20px;
  border-radius: 6px;
  width: 75%;
  box-sizing: border-box;
  margin: auto;
  margin-bottom: 15px;
}
.school-card .data {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.data img {
  width: 16%;
}
.data button {
  padding: 6px 8px;
  font-size: 14px;
  border: 1px solid #000;
  border-radius: 10px;
  background: #fff;
  font-weight: 800;
}
.data span {
  font-size: 16px;
  font-weight: 700;
  width: 112px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.data .action {
  width: 30%;
  display: flex;
  align-items: center;
  gap: 12px;
}
</style>
