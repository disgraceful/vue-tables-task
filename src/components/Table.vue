<template>
  <div>
    <b-table hover responsive="md" :items="items" @row-hovered="hoverRow">
      <template #cell(email)="row">
        <div class="row">
          {{ row.value }}
          <div class="popup-container" v-show="hoveredRow == row.item">
            <div class="popup-container--icon mx-2">
              <b-icon
                v-b-modal.modal
                icon="person-plus"
                variant="success"
                font-scale="1.8"
              ></b-icon>
            </div>
            <div class="popup-container--icon mx-2">
              <b-icon icon="pencil" font-scale="1.5"></b-icon>
            </div>
            <div class="popup-container--icon mx-2">
              <b-icon
                icon="x-circle"
                variant="danger"
                font-scale="1.5"
              ></b-icon>
            </div>
          </div>
        </div>
      </template>
    </b-table>
    <record-modal></record-modal>
  </div>
</template>

<script>
import RecordModal from "./Modal";

export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  components: {
    "record-modal": RecordModal,
  },

  data() {
    return {
      showModal: false,
      hoveredRow: null,
      hovered: false,
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
.row {
  position: relative;
}

.popup-container {
  position: absolute;
  top: 0;
  right: 1rem;
  display: flex;
  justify-content: flex-end;
  align-items: baseline;

  .popup-container--icon > * {
    cursor: pointer;
  }
}

.b-table tr:hover .popup-container {
  display: flex;
}

.b-table > tbody > tr:not(:hover) .popup-container {
  display: none;
}
</style>
