<template>
  <div class="form-container">
    <Avatar />
    <form @submit.prevent="handleSubmit">
      <Input
        id="name"
        v-model="form.name"
        :disabled="!isEditing"
        type="text"
        placeholder="Name"
        :required="true"
        :error="errors.name"
      />
      <Input
        id="lastname"
        v-model="form.lastname"
        :disabled="!isEditing"
        type="text"
        placeholder="Lastname"
        :required="true"
        :error="errors.lastname"
      />
      <Input
        id="titlejob"
        v-model="form.titlejob"
        :disabled="!isEditing"
        type="text"
        placeholder="Job Title"
      />
      <Input
        id="phone"
        v-model="form.phone"
        :disabled="!isEditing"
        type="tel"
        placeholder="Phone"
        :required="true"
        :error="errors.phone"
      />
      <Input
        id="email"
        v-model="form.email"
        :disabled="!isEditing"
        type="email"
        placeholder="Email"
      />
      <Input
        id="address"
        v-model="form.address"
        :disabled="!isEditing"
        type="text"
        placeholder="Address"
      />
      <Input
        id="pitch"
        v-model="form.pitch"
        :disabled="!isEditing"
        type="text"
        placeholder="Pitch"
      />
      <RadioButton v-model="form.radioBtn" :disabled="!isEditing" />
      <FormList
        ref="interests"
        :disabled="!isEditing"
        name="The scopes of your interest:"
      />
      <FormList
        ref="hobbies"
        :disabled="!isEditing"
        name="Potential interests:"
      />
      <FormLinks ref="links" :disabled="!isEditing" name="Your links:" />
      <div class="form-actions">
        <button v-if="isEditing" type="submit">Save</button>
        <button v-if="isEditing" type="button" @click="resetForm">
          Cancel
        </button>
        <button v-else type="button" @click="editForm">Edit</button>
      </div>
    </form>
  </div>
</template>

<script>
import Avatar from "./Avatar.vue";
import Input from "./Input.vue";
import RadioButton from "./RadioButton.vue";
import FormList from "./FormList.vue";
import FormLinks from "./FormLinks.vue";

export default {
  components: {
    Avatar,
    Input,
    RadioButton,
    FormList,
    FormLinks,
  },
  data() {
    return {
      form: {
        name: "",
        lastname: "",
        titlejob: "",
        phone: "",
        email: "",
        address: "",
        pitch: "",
        radioBtn: "private",
      },
      scopes: [],
      hobbies: [],
      links: [],
      errors: {
        name: "",
        lastname: "",
        phone: "",
        titlejob: "",
        address: "",
        scopes: "",
        links: "",
      },
      isEditing: true,
      initialData: null,
    };
  },
  created() {
    const savedData = JSON.parse(localStorage.getItem("formData"));
    if (savedData) {
      this.form = savedData.form || this.form;
      this.scopes = savedData.scopes || [];
      this.hobbies = savedData.hobbies || [];
      this.links = savedData.links || [];
      this.isEditing = false;
    }
    this.initialData = JSON.parse(JSON.stringify(this.form));
  },
  methods: {
    handleSubmit() {
      this.errors = {};

      if (!this.form.name) {
        this.errors.name = "Name is required.";
      } else if (
        !/^[A-Za-zА-Яа-яЁё\s\-]+$/.test(this.form.name) ||
        this.form.name.length < 2 ||
        this.form.name.length > 50
      ) {
        this.errors.name =
          "Name must be between 2 and 50 characters and contain only letters, spaces, and hyphens.";
      }

      if (!this.form.lastname) {
        this.errors.lastname = "Lastname is required.";
      } else if (
        !/^[A-Za-zА-Яа-яЁё\s\-]+$/.test(this.form.lastname) ||
        this.form.lastname.length < 2 ||
        this.form.lastname.length > 50
      ) {
        this.errors.lastname =
          "Lastname must be between 2 and 50 characters and contain only letters, spaces, and hyphens.";
      }

      if (
        this.form.titlejob &&
        (this.form.titlejob.length > 100 ||
          !/^[A-Za-zА-Яа-яЁё0-9\s\-]+$/.test(this.form.titlejob))
      ) {
        this.errors.titlejob =
          "Job title must be up to 100 characters and can contain letters, numbers, and spaces.";
      }

      if (!this.form.phone) {
        this.errors.phone = "Phone is required.";
      } else if (!/^\+[\d]{10,15}$/.test(this.form.phone)) {
        this.errors.phone = "Phone must be in the format +country code";
      }

      if (this.form.address && this.form.address.length > 200) {
        this.errors.address = "Address must be up to 200 characters.";
      }

      if (this.scopes.length > 10) {
        this.errors.scopes = "You can select up to 10 interests.";
      } else {
        this.scopes.forEach((scope) => {
          if (
            !/^[A-Za-zА-Яа-яЁё0-9\s,.\-]+$/.test(scope) ||
            scope.length > 30
          ) {
            this.errors.scopes =
              "Interests must be no longer than 30 characters and can only contain letters, numbers, spaces, commas, and periods.";
          }
        });
      }

      this.links.forEach((link) => {
        if (link.length > 200 || !/^(https?:\/\/)/.test(link)) {
          this.errors.links =
            "Links must be a valid URL starting with http:// or https:// and up to 200 characters long.";
        }
      });

      if (Object.keys(this.errors).length === 0) {
        this.scopes = this.$refs.interests.getItems();
        this.hobbies = this.$refs.hobbies.getItems();
        this.links = this.$refs.links.getItems();

        const formData = {
          form: this.form,
          scopes: this.scopes,
          hobbies: this.hobbies,
          links: this.links,
        };

        localStorage.setItem("formData", JSON.stringify(formData));

        this.isEditing = false;
      }
    },

    resetForm() {
      this.form = JSON.parse(JSON.stringify(this.initialData));
      this.errors = {};
      this.isEditing = false;
    },

    editForm() {
      this.isEditing = true;
    },
  },
};
</script>

<style>
.form-container {
  padding: 106px 48px 40px;
  background: linear-gradient(180deg, #e9f2f3 0%, #a6c5e3 100%);
  border-radius: 24px;
  max-width: 792px;
  width: 100%;
  box-sizing: border-box;
  margin: 0 0 0 auto;
}

.form-actions {
  margin-top: 40px;
  display: flex;
  gap: 10px;
  justify-content: end;
}

.form-actions button {
  padding: 10px 20px;
  border: none;
  font-size: 20px;
  font-weight: 600;
  border-radius: 4px;
  cursor: pointer;
}

button[type="submit"] {
  background: #4caf50;
  color: #fff;
}

button[type="button"] {
  background: #f44336;
  color: #fff;
}

button[type="button"]:last-child {
  background: #2196f3;
}
.input-wrapper {
  position: relative;
}
.input-wrapper p {
  position: absolute;
  left: 0;
  bottom: -15px;
}
@media screen and (max-width: 1167px) {
  .form-container {
    margin: 0 auto;
  }
}
@media screen and (max-width: 767px) {
  .form-container {
    padding: 30px 16px;
  }
}
</style>
