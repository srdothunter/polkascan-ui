<template>
  <div class="transfer-item-wrapper">
    <div class="transfer-item-top space-between align-items-center">
      <div class="left align-items-center">
        <div class="label">Hash</div>
        <el-tooltip class="item" effect="light" :content="transferData.hash" placement="top-start">
          <div
            class="value hash-v"
            @click="$router.push(`/extrinsic/${transferData.hash}`)"
          >{{transferData.hash}}</div>
        </el-tooltip>
      </div>
      <div class="right">{{transferData.block_timestamp|timeAgo(currentTime)}}</div>
    </div>
    <div class="transfer-item-bottom space-between align-items-center">
      <div class="left align-items-center">
        <div class="label">From</div>
        <div class="value">
          <el-tooltip
            class="item"
            effect="light"
            :content="transferData.from"
            placement="top-start"
          >
            <div
              class="from"
              @click="$router.push(`/account/${transferData.from}`)"
            >{{transferData.from}}</div>
          </el-tooltip>
          <div class="separator">&nbsp;To&nbsp;&nbsp;</div>
          <el-tooltip class="item" effect="light" :content="transferData.to" placement="top-start">
            <div class="to" @click="$router.push(`/account/${transferData.to}`)">{{transferData.to}}</div>
          </el-tooltip>
        </div>
      </div>
      <div class="right">{{`${transferData.amount} RC`}}</div>
    </div>
  </div>
</template>

<script>
import { timeAgo } from "Utils/filters";
import { mapState } from "vuex";

export default {
  props: {
    transferData: {
      type: Object,
      required: true
    },
    currentTime: {
      type: Number
    }
  },
  computed: {
    ...mapState({
      sourceSelected: state => state.global.sourceSelected
    })
  },
  filters: {
    timeAgo
  },
  methods: {}
};
</script>

<style lang="scss" scoped>
.transfer-item-wrapper {
  box-sizing: border-box;
  height: 80px;
  padding: 16px 0 20px;
  .transfer-item-top,
  .transfer-item-bottom {
    .left {
      .label {
        width: 59px;
      }
    }
  }
  .transfer-item-top {
    // transform: translateY(-3px);
    .left {
      .label {
        font-size: 13px;
        font-weight: 600;
        color: rgba(19, 18, 18, 1);
      }
      .value {
        font-size: 14px;
        font-weight: 600;
        color: var(--main-color);
        cursor: pointer;
        width: 308px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
    }
    .right {
      font-size: 14px;
      font-weight: 600;
      color: rgba(152, 149, 159, 1);
    }
  }
  .transfer-item-bottom {
    padding-top: 7px;
    font-size: 12px;
    .left {
      .label {
        font-weight: 600;
        color: rgba(152, 149, 159, 1);
      }
      .value {
        display: flex;
        .from,
        .to {
          cursor: pointer;
          font-weight: 400;
          color: var(--main-color);
          width: 86px;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
        }
        .separator {
          font-weight: 600;
          color: rgba(152, 149, 159, 1);
        }
      }
    }
    .right {
      font-size: 14px;
      font-weight: bold;
      color: var(--main-color);
      line-height: 20px;
    }
  }
}
</style>
