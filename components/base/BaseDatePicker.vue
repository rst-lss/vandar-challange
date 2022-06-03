<template>
  <v-dialog v-model="dialog" max-width="500">
    <template #activator="{ on, attrs }">
      <!-- activator (visible as input) -->
      <v-btn
        class="dialog-activator grey--text text--darken-2 mb-3"
        elevation="0"
        height="38"
        block
        dark
        v-bind="attrs"
        v-on="on"
      >
        {{ date.day + '/' + date.month + '/' + date.year }}
      </v-btn>
    </template>

    <div class="date-picker">
      <h3 class="pa-1 mb-4">تاریخ مورد نظر را انتخاب کنید</h3>

      <!-- date selects -->
      <div class="d-flex justify-space-between">
        <v-select
          v-model="date.year"
          :items="years"
          label="سال"
          outlined
        ></v-select>
        <v-select
          v-model="date.month"
          :items="months"
          label="ماه"
          outlined
        ></v-select>
        <v-select
          v-model="date.day"
          :items="days"
          label="روز"
          outlined
        ></v-select>
      </div>

      <!-- submit button -->
      <v-btn class="white--text" color="#4C9F87" @click="submit">
        ذخیره تاریخ
      </v-btn>
    </div>
  </v-dialog>
</template>

<script>
export default {
  name: 'BaseDatePicker',
  data() {
    return {
      dialog: false,
      date: {
        day: 1,
        month: 1,
        year: 1396,
      },
      years: [],
      months: [],
      days: [],
    }
  },
  created() {
    for (let i = 1396; i < 1401; i++) {
      this.years.push(i)
    }
    for (let i = 1; i < 13; i++) {
      this.months.push(i)
    }
    for (let i = 1; i < 32; i++) {
      this.days.push(i)
    }
  },
  methods: {
    submit() {
      this.$emit('submit', this.date)
      this.dialog = false
    },
  },
}
</script>

<style lang="scss" scoped>
.date-picker {
  padding: 1rem;
  background-color: #fff;
  max-width: 500px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}

.dialog-activator {
  border: 1px solid rgb(213, 213, 213) !important;

  &.theme--dark.v-btn.v-btn--has-bg {
    background-color: white !important;
  }
}
</style>
