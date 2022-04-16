<template>
  <div class="py-4">
    <div class="container">
      <div class="form">
        <form v-on:submit.prevent="submitForm">
          <div class="field-control">
            <label class="label">Nama :</label>
            <input
              type="text"
              class="input"
              placeholder="Masukkan nama"
              v-model="form.name"
            />
          </div>
          <div class="field-control">
            <label class="label">Pesan :</label>
            <textarea
              name=""
              cols="30"
              rows="10"
              class="textarea"
              placeholder="Masukkan Pesan"
              v-model="form.message"
            ></textarea>
          </div>
          <div class="field-control">
            <label for="" class="label">Prioritas</label>
            <select class="input" v-model="form.priority_type">
              <option
                v-for="(option, i) in priorityOptions"
                :key="i"
                v-bind:value="option.option"
              >
                {{ option.option }}
              </option>
            </select>
          </div>
          <div class="field-control">
            <input type="checkbox" v-model="form.agreement" />
            <label class="label">Anda telah menyetujui</label>
          </div>
          <div class="field-control">
            <button class="btn btn-primary" type="submit">SUBMIT</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: "",
        message: "",
        priority: "",
        agreement: false,
        priority_type: "",
      },
      priorityOptions: [
        { option: "Tidak ada prioritas", value: "" },
        { option: "Rendah", value: "low" },
        { option: "Tinggi", value: "high" },
      ],
    };
  },
  methods: {
    submitForm() {
      console.log(this.form);
    },
  },
};
</script>
