<template>
  <div v-if="contact" class="page">
    <h4>Tạo Liên Hệ</h4>
    <ContactForm :contact="contact" @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
  components: {
    ContactForm,
  },

  data() {
    return {
      contact: {
        name: " ",
        email: " ",
        address: " ",
        phone: " ",
      },
      message: "",
    };
  },
  methods: {
    async getContact(id) {
      try {
        this.contact = await ContactService.get(id);
      } catch (error) {
        console.log(error);
        // Chuyển sang trang NotFound đồng thời giữ cho URL không đổi
        this.$router.push({
          name: "notfound",
          params: {
            pathMatch: this.$route.path.split("/").slice(1),
          },
          query: this.$route.query,
          hash: this.$route.hash,
        });
      }
    },
    async addContact(data) {
      try {
        await ContactService.create(data);
        this.message = "Liên hệ được tạo thành công.";
      } catch (error) {
        console.log(error);
      }
    },
  },
  // created() {
  //   this.getContact(this.id);
  //   this.message = "";
  // },
};
</script>
