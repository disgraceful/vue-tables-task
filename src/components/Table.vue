<template>
  <b-table hover responsive="md" :items="items" @row-hovered="hoverRow">
    <template #cell(email)="row">
      {{ row.value }}
      <div class="popup-container" v-show="hoveredRow == row.item">
        <div class="popup-container--icon mx-2">
          <b-icon
            icon="person-plus"
            variant="success"
            font-scale="1.8"
          ></b-icon>
        </div>
        <div class="popup-container--icon mx-2">
          <b-icon icon="pencil" font-scale="1.5"></b-icon>
        </div>
        <div class="popup-container--icon mx-2">
          <b-icon icon="x-circle" variant="danger" font-scale="1.5"></b-icon>
        </div>
      </div>
    </template>
  </b-table>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      hoveredRow: null,
    };
  },
  methods: {
    hoverRow(row) {
      console.log(row);
      this.hoveredRow = row;
    },
  },
};
</script>

<style lang="scss" scoped>
.popup-container {
  display: flex;
  justify-content: flex-end;
  align-items: baseline;
}
</style>
