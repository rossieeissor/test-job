<template>
  <div class="profile__container">
    <div v-if="profileIsLoading" class="profile__loading">
      Loading profile ...
    </div>
    <div v-else class="profile__info">
      <img
        class="profile__info--avatar"
        :src="trimAvatarURL(profile.avatar)"
        alt=""
      />
      <div class="profile__info--data">
        <p>Name: {{ profile.first_name }}</p>
        <p>Age: {{ getAge(profile.date_of_birth) }}</p>
        <p>Title: {{ profile.employment.title }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    profile: {
      type: Object,
      required: true,
    },
    profileIsLoading: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    trimAvatarURL(url) {
      if (url) {
        return url.match(/https:\/\/robohash\.org\/[a-z]*/)[0];
      }
    },
    getAge(dateString) {
      const today = new Date();
      const birthDate = new Date(dateString);
      let age = today.getFullYear() - birthDate.getFullYear();
      const m = today.getMonth() - birthDate.getMonth();
      if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) {
        age--;
      }
      return age;
    },
  },
};
</script>

<style scoped>
.profile__container {
  display: flex;
  justify-content: center;
  align-content: center;
  margin: 0 auto;
  min-width: 100%;
}

.profile__loading {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
}

.profile__info {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 100%;
  gap: 20px;
  height: 100%;
}

.profile__info--avatar {
  max-height: 100%;
  justify-self: flex-end;
}

.profile__info--data {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: center;
  gap: 10%;
  font-size: 2rem;
}

@media screen and (max-width: 768px) {
  .profile__info {
    grid-template-columns: auto;
    grid-template-rows: auto auto;
    gap: 10px;
  }

  .profile__info--avatar {
    justify-self: center;
    width: 50%;
    height: auto;
  }

  .profile__info--data {
    gap: 5px;
    font-size: 1.6rem;
  }

  .profile__info--data {
    text-align: center;
  }
}
</style>
