<template>
  <div class="py-4">
    <div class="container">
      <div
        class="title border-bottom d-flex align-items-center justify-content-between py-2"
      >
        <h5>Task</h5>

        <div class="d-flex align-items-center ms-auto">
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />

          <div class="d-flex align-items-center">
            <button
              class="btn btn-outline-secondary py-1 px-3"
              @click="isGrid = !isGrid"
            >
              {{ isGrid ? "Grid" : "List" }}
            </button>
          </div>
        </div>
      </div>

      <div class="list-task row">
        <CardItem
          v-for="(task, i) in resultQuery"
          :key="i"
          :task="task"
          :isGrid="isGrid"
        />
      </div>
      <h5>Form</h5>
      <div class="form">
        <form v-on:submit.prevent="submitForm">
          <div class="field-control">
            <label class="label">Judul :</label>
            <div class="control">
              <input
                name="title"
                type="text"
                class="input"
                placeholder="Masukkan Judul"
                v-model="tambah.title"
              />
            </div>
          </div>
          <div class="field-control">
            <label class="label">Deskripsi :</label>
            <div class="control">
              <textarea
                name="desctiption"
                cols="25"
                rows="3"
                class="textarea"
                placeholder="Masukkan Deskripsi"
                v-model="tambah.description"
              ></textarea>
            </div>
          </div>
          <div class="field-control">
            <label class="label">Kategori :</label>
            <div class="control">
              <select name="category" class="input" v-model="tambah.category">
                <option disabled value="null">Pilih Kategori</option>
                <option
                  v-for="(option, i) in categoryOptions"
                  :key="i"
                  v-bind:value="option.option"
                >
                  {{ option.option }}
                </option>
              </select>
            </div>
          </div>
          <br />
          <div class="field-control">
            <div class="control">
              <button class="btn btn-success" type="submit">Tambah</button>
            </div>
          </div>
        </form>
        <!-- <div class="column">
          <section class="section" id="results">
            <div class="box">
              <ul style="list-style-type: none">
                <li v-for="(task, i) in tambah" v-bind:key="i">
                  <strong>{{ i }} :</strong> {{ task }}
                </li>
              </ul>
            </div>
          </section>
        </div> -->
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },
  data() {
    return {
      tambah: {
        title: null,
        description: null,
        category: null,
      },

      searchQuery: "",

      isGrid: false,

      arrayOfObjects: [],

      tasks: [
        {
          title: "Lemper",
          description: "Lemper Enak",
          isDone: false,
          category: "Makanan",
          selected: "",
        },
        {
          title: "Teh Bohai",
          description: "Teh Bohai Seger",
          isDone: false,
          category: "Minuman",
          selected: "",
        },
        {
          title: "Mintz",
          description: "Mintz Seger",
          isDone: false,
          category: "Permen",
          selected: "",
        },
        {
          title: "Jagung",
          description: "Jagung Di Bakar",
          isDone: false,
          category: "Makanan",
        },
        {
          title: "Cincau",
          description: "Cincau Bikin Lengket",
          isDone: false,
          category: "Minuman",
        },
        {
          title: "Kopiko",
          description: "Kopiko Adem",
          isDone: false,
          category: "Permen",
        },
      ],
      categoryOptions: [
        { option: "Makanan", value: "makanan" },
        { option: "Minuman", value: "minuman" },
        { option: "Permen", value: "permen" },
      ],
    };
  },

  methods: {
    submitForm() {
      this.tasks.push({
        title: this.tambah.title,
        description: this.tambah.description,
        isDone: this.tambah.isDone,
        category: this.tambah.category,
      });
    },
  },

  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else {
        console.log(this.tasks);
        return this.tasks;
      }
    },
  },
};
</script>

<style>
.my-dropdown-toggle {
  border-radius: 5px;
}
#results {
  position: fixed;
  right: 60%;
  top: 60%;
}
</style>
