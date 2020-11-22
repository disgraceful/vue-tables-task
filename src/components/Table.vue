<template>
  <div>
    <b-table hover responsive="md" :items="items" @row-hovered="hoverRow">
      <template #cell(email)="row">
        <div class="row">
          {{ row.value }}
          <div class="popup-container">
            <div class="popup-container--icon mx-2">
              <b-icon
                v-b-modal.table-modal
                @click="useFnc = addFnc.bind(this, hoveredIndex + 1)"
                icon="person-plus"
                variant="success"
                font-scale="1.8"
              ></b-icon>
            </div>
            <div class="popup-container--icon mx-2">
              <b-icon
                v-b-modal.table-modal
                @click="
                  (useFnc = editFnc.bind(this, hoveredIndex)), (mode = 'edit')
                "
                icon="pencil"
                font-scale="1.5"
              ></b-icon>
            </div>
            <div class="popup-container--icon mx-2">
              <b-icon
                v-b-modal.delete-modal
                icon="x-circle"
                variant="danger"
                font-scale="1.5"
              ></b-icon>
            </div>
          </div>
        </div>
      </template>
    </b-table>
    <record-modal
      id="table-modal"
      :mode="mode"
      :user="hoveredRow"
      :okFnc="useFnc"
    >
    </record-modal>
    <confirm-modal
      id="delete-modal"
      :msg="deleteText"
      :okFnc="deleteFnc.bind(this, hoveredRow)"
    >
      <p v-text="deleteText"></p>
    </confirm-modal>
  </div>
</template>

<script>
import RecordModal from "./Modal";
import ConfirmModal from "./ConfirmModal";

export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    addFnc: Function,
    editFnc: Function,
    deleteFnc: Function,
  },

  components: {
    "record-modal": RecordModal,
    "confirm-modal": ConfirmModal,
  },

  data() {
    return {
      hoveredRow: null,
      hoveredIndex: -1,
      useFnc: null,
      mode: "",
    };
  },

  computed: {
    deleteText() {
      return `Are you sure you want to delete user ${
        this.hoveredRow ? this.hoveredRow.email : ""
      }?`;
    },
  },
  methods: {
    hoverRow(row, index) {
      this.hoveredIndex = index;
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
