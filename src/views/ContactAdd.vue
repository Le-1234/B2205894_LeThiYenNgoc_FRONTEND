<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="contact" @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
import { useRouter } from 'vue-router';

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      // Khởi tạo một đối tượng contact trống
      contact: {
        name: '',
        email: '',
        address: '',
        phone: '',
        favorite: false,
      },
      message: "",
    };
  },
  methods: {
    // Phương thức để thêm liên hệ mới
    async addContact(data) {
      try {
        await ContactService.create(data);  
        alert("Liên hệ đã được thêm thành công.");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
        this.message = "Có lỗi khi thêm liên hệ, vui lòng thử lại.";
      }
    },
  },
};
</script>

