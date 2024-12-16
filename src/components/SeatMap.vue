<template>
  <div>
    <div class="seat-map">
      <!-- 座席リスト -->
      <div
        v-for="seat in seats"
        :key="seat.id"
        class="seat"
        @click="openModal(seat)"
      >
        {{ seat.name || '' }}
      </div>
    </div>

    <!-- モーダル -->
    <div class="modal" v-if="isModalOpen">
      <div class="modal-content">
        <button class="close-button" @click="closeModal">
          <i class="fas fa-times"></i>
        </button>
        <h2>名前</h2>
        <form @submit.prevent="updateSeatName">
          <input
            type="text"
            v-model="currentSeatName"
            placeholder="名前を入力する"
            maxlength="8"
          />
          <button type="submit" class="create-btn">登録</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      seats: [
        { id: "A1", name: "" },
        { id: "A2", name: "" },
        { id: "A3", name: "" },
        { id: "A4", name: "" },
        { id: "B1", name: "" },
        { id: "B2", name: "" },
        { id: "B3", name: "" },
        { id: "B4", name: "" },
      ],
      isModalOpen: false,
      selectedSeat: null,
      currentSeatName: "",
    };
  },
  methods: {
    openModal(seat) {
      this.selectedSeat = seat;
      this.currentSeatName = seat.name || "";
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
    },
    updateSeatName() {
      if (this.selectedSeat && this.currentSeatName.trim() !== "") {
        this.selectedSeat.name = this.currentSeatName.trim();
        this.closeModal();
      }
    },
  },
};
</script>

<style scoped>
/* 全体スタイル */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #f9f9f9;
}

/* 座席表スタイル */
.seat-map {
  display: grid;
  grid-template-columns: repeat(4, 80px); /* 座席を横4列に配置 */
  gap: 1px;
  margin: 20px;
}

/* 各座席スタイル */
.seat {
  width: 80px;
  height: 80px;
  background-color: #cce7ff;
  border: 1px solid #007bff;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  font-size: 14px;
  color: #007bff;
}

.seat:hover {
  background-color: #007bff;
  color: #fff;
}

/* モーダルのスタイル */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  position: relative;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

input {
  width: 80%;
  padding: 10px;
  margin-bottom: 10px;
  font-size: 16px;
}

.create-btn {
  padding: 10px 20px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

.create-btn:hover {
  background-color: #0056b3;
}


/* 閉じるボタン */
.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 10px;
  cursor: pointer;
}
</style>