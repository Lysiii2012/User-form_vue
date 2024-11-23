<template>
  <div class="avatar-container" @click="triggerFileInput">
    <div class="avatar-placeholder">
      <img
        :src="avatarSrc"
        alt="avatar"
        class="avatar-img"
        :class="{ 'updated-avatar': isAvatarUpdated }"
      />
    </div>
    <input
      ref="avatarInput"
      type="file"
      id="avatarInput"
      class="avatar-input"
      @change="handleFileUpload"
      accept="image/*"
    />
  </div>
</template>

<script>
import DefaultAvatar from "../../assets/media/avatar.svg";

export default {
  data() {
    return {
      avatarSrc: localStorage.getItem("avatar") || DefaultAvatar,
      isAvatarUpdated: localStorage.getItem("isAvatarUpdated") === "true",
    };
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();

        reader.onload = (e) => {
          this.avatarSrc = e.target.result;
          localStorage.setItem("avatar", e.target.result);

          if (!this.isAvatarUpdated) {
            this.isAvatarUpdated = true;
            localStorage.setItem("isAvatarUpdated", "true");
          }
        };

        reader.readAsDataURL(file);
      }
    },
    triggerFileInput() {
      const fileInput = this.$refs.avatarInput;
      if (fileInput) {
        fileInput.click();
      } else {
        console.error("Ref для avatarInput не найден.");
      }
    },
  },
};
</script>

<style scoped>
.avatar-container {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #d9d9d9;
  margin: 0 auto 28px;
  position: relative;
  cursor: pointer;
}

.avatar-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.avatar-placeholder img.avatar-img {
  width: 42px;
  height: 42px;
}
.avatar-placeholder img {
  max-width: 100%;
  max-height: 100%;
  object-fit: cover;
  object-position: center;
  transition: border 0.3s ease;
}

.avatar-placeholder img.updated-avatar {
  max-width: 100%;
  max-height: 100%;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: border 0.3s ease;
}

.avatar-input {
  display: none;
}
</style>
