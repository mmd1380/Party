<template>
<div>
  <form v-if="section == 'main'" style="direction: ltr">
    <v-row>
      <v-col>
        <v-menu
          ref="endMenu"
          :close-on-content-click="false"
          :return-value.sync="Party.BirthDate"
          offset-y
          min-width="200px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="Party.BirthDate"
              label="تاریخ تولد"
              prepend-icon="mdi-calendar"
              reverse
              readonly
              v-bind="attrs"
              class="pr-1"
              v-on="on"
              :rules="[() => !!Party.BirthDate || 'این قسمت باید پر شود']"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" no-title scrollable>
            <v-spacer></v-spacer>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.isActive = false"
            >
              Cancel
            </v-btn>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.save(date)"
            >
              OK
            </v-btn>
          </v-date-picker>
        </v-menu>
      </v-col>
      <v-col>
        <v-text-field
          v-model="Party.NationalID"
          label="کد ملی"
          counter="10"
          maxlength="10"
          required
          reverse
          hint="e.g : 002-144449-1"
          :rules="[() => !!Party.NationalID || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-autocomplete
          style="direction: ltr"
          v-model="Party.nation"
          :items="Party.nations"
          label="ملیت"
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.nation || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
    </v-row>

    <br />

    <v-row
      style="
        direction: rtl;
        font-weight: bolder;
        font-size: large;
        padding-bottom: 15px;
      "
    >
      پس از استعلام
    </v-row>
    <v-row
      style="border-top: solid #aeaeae 1px; background-color: #ebf6ff"
      class="py-10"
    >
      <v-col>
        <v-text-field
          class="rtl"
          v-model="Party.Lname"
          label="نام خانوادگی"
          required
          reverse
          :rules="[() => !!Party.Lname || 'این قسمت باید پر شود']"
          @input="$v.Lname.$touch()"
          @blur="$v.Lname.$touch()"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-text-field
          class="rtl"
          v-model="Party.name"
          label="نام"
          required
          reverse
          @input="$v.name.$touch()"
          @blur="$v.name.$touch()"
          :rules="[() => !!Party.name || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-text-field
          class="rtl"
          v-model="Party.FatherName"
          label="نام پدر"
          required
          reverse
          :rules="[() => !!Party.FatherName || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>
    </v-row>

    <v-row style="background-color: #ebf6ff" class="py-10">
      <v-col>
        <v-autocomplete
          v-model="Party.IssuanceCity"
          :items="Party.cities"
          label="شهر محل صدور شناسنامه"
          required
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.IssuanceCity || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
      <v-col>
        <v-menu
          ref="endMenu"
          :close-on-content-click="false"
          :return-value.sync="Party.IssuanceDate"
          offset-y
          min-width="200px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="Party.IssuanceDate"
              label="تاریخ صدور شناسنامه"
              prepend-icon="mdi-calendar"
              reverse
              readonly
              v-bind="attrs"
              class="pr-1"
              v-on="on"
              :rules="[() => !!Party.IssuanceDate || 'این قسمت باید پر شود']"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" no-title scrollable>
            <v-spacer></v-spacer>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.isActive = false"
            >
              Cancel
            </v-btn>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.save(date)"
            >
              OK
            </v-btn>
          </v-date-picker>
        </v-menu>
      </v-col>
      <v-col>
        <v-text-field
          class="rtl"
          v-model="Party.IdNo"
          label="شماره شناسنامه"
          required
          reverse
          :rules="[() => !!Party.IdNo || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>
    </v-row>

    <v-row
      style="
        border-bottom: solid #aeaeae 1px;
        background-color: #ebf6ff;
      "
      class="py-10"
    >
      <v-col>
        <v-autocomplete
          v-model="Party.Prefix"
          :items="Party.Prefixes"
          label="پیشوند"
          required
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.Prefix || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
      <v-col>
        <v-autocomplete
          v-model="Party.Gender"
          :items="Party.Genders"
          label="جنسیت"
          required
          clearable
          dense
          reverse
          filled
        ></v-autocomplete>
      </v-col>
      <v-col>
        <v-autocomplete
          v-model="Party.BirthCity"
          :items="Party.cities"
          label="شهر محل تولد"
          required
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.BirthCity || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
    </v-row>

    <v-row class="py-10">
      <v-col>
        <v-autocomplete
          v-model="Party.LivingCity"
          :items="Party.cities"
          label="شهر محل سکونت"
          required
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.LivingCity || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
      <v-col>
        <v-text-field
          v-model="Party.NationalID"
          label="نام مستعار"
          counter="20"
          required
          reverse
          :rules="[() => !!Party.NationalID || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-autocomplete
          style="direction: ltr"
          v-model="Party.Religion"
          :items="Party.Religions"
          label="دین"
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.Religion || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <v-file-input
          v-model="files"
          color="deep-purple accent-4"
          counter
          label="آپلود فایل عکس"
          multiple
          placeholder="فایل خود را آپلود کنید"
          prepend-icon="mdi-paperclip"
          outlined
        >
          <template v-slot:selection="{ index, text }">
            <v-chip
              v-show="index < 2"
              color="deep-purple accent-4"
              dark
              label
              large
            >
              {{ text }}
            </v-chip>
            <span
              v-else-show="index === 2"
              class="overline grey--text text--darken-3 mx-2"
            >
              +{{ files.length - 2 }} File(s)
            </span>
          </template>
        </v-file-input>
      </v-col>
    </v-row>
  </form>
  <form v-else-if="section == 'complement'"  style="direction: ltr">
    <v-row>
      <v-col>
        <v-menu
          ref="endMenu"
          :close-on-content-click="false"
          :return-value.sync="Party.RetirementDate"
          offset-y
          min-width="200px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="Party.RetirementDate"
              label="تاریخ تقریبی بازنشستگی"
              prepend-icon="mdi-calendar"
              reverse
              readonly
              v-bind="attrs"
              class="pr-1"
              v-on="on"
              :rules="[() => !!Party.RetirementDate || 'این قسمت باید پر شود']"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" no-title scrollable>
            <v-spacer></v-spacer>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.isActive = false"
            >
              Cancel
            </v-btn>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.save(date)"
            >
              OK
            </v-btn>
          </v-date-picker>
        </v-menu>
      </v-col>
      <v-col>
        <v-text-field
          v-model="Party.ChildrenNo"
          label="تعداد فرندان"
          type="number"
          min="0"
          max="10"
          required
          reverse
          :rules="[() => !!Party.ChildrenNo || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>

      <v-col>
        <v-combobox
          v-model="Party.Role"
          :items="Party.Roles"
          label="نقش ها"
          multiple
          reverse
          chips
          large
          :rules="[() => Party.Role.length != 0 || 'این قسمت باید پر شود']"
        ></v-combobox>
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <v-menu
          ref="endMenu"
          :close-on-content-click="false"
          :return-value.sync="Party.PassportExpiryDate"
          offset-y
          min-width="200px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-text-field
              v-model="Party.PassportExpiryDate"
              label="تاریخ انقضا پاسپورت"
              prepend-icon="mdi-calendar"
              reverse
              readonly
              v-bind="attrs"
              class="pr-1"
              v-on="on"
              :rules="[() => !!Party.PassportExpiryDate || 'این قسمت باید پر شود']"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" no-title scrollable>
            <v-spacer></v-spacer>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.isActive = false"
            >
              Cancel
            </v-btn>
            <v-btn
              text
              color="primary"
              @click="$refs.endMenu.save(date)"
            >
              OK
            </v-btn>
          </v-date-picker>
        </v-menu>
      </v-col>

      <v-col>
        <v-text-field
          v-model="Party.PassportNo"
          label="شماره پاسپورت"
          counter="10"
          maxlength="10"
          required
          reverse
          :rules="[() => !!Party.PassportNo || 'این قسمت باید پر شود']"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-autocomplete
          style="direction: ltr"
          v-model="Party.Degree"
          :items="Party.Degrees"
          label="مدرک تحصیلی"
          clearable
          dense
          reverse
          filled
          :rules="[() => !!Party.Degree || 'این قسمت باید پر شود']"
        ></v-autocomplete>
      </v-col>
    </v-row>
  </form>
  <form v-else-if="section == 'communicate'">
    <v-row>
      <v-col>
        <v-row justshowy="center">
          <v-col cols="8">
            <v-combobox
              v-model="Party.CommunicateWay"
              :items="Party.CommunicationWays"
              label="کانال تماس"
              multiple
              reverse
              chips
              large
              :rules="[() => Party.CommunicateWay.length != 0 || 'این قسمت باید پر شود']"
            ></v-combobox>
          </v-col>
        </v-row>
        <v-row justshowy="center">
          <v-col cols="6" v-for="(input) in Party.CommunicateWay" :key="input">
            <v-text-field
              :label="input"
              filled
              v-model="Party.CommunicateData[input]"
              reverse
              chips
              :type="inputType(input)"
              :rules="[v => !!v || 'این قسمت باید پر شود']"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row justshowy="center">
          <v-col cols="12">
            <div class="text-center">
              <v-btn
                v-show="Party.CommunicateWay.length !== 0"
                large
                color="primary"
                @click="validate()"
              >ثبت</v-btn>
            </div>
          </v-col>
        </v-row>
      </v-col>  
    </v-row>
  </form>
  <form ref="form" v-else-if="section == 'communicate'" style="direction: ltr">
    
  </form>
  <form v-else-if="section == 'address'" style="direction: ltr">
    <v-row>
    <v-col>
    <v-data-table
        :headers="headers"
        :items="Parties"
        class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar
            flat
        >

          <v-dialog
              v-model="dialog"
              max-width="500px"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                  color="primary"
                  dark
                  class="mb-2"
                  v-bind="attrs"
                  v-on="on"
              >
                آدرس جدید
              </v-btn>
            </template>
            <v-card>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col
                        cols="12"

                    >

                      <v-autocomplete
                          v-model="editedItem.AddressType"
                          label="AddressType"
                          :items="editedItem.AddressType"
                          required
                          clearable
                          dense
                          reverse
                          filled

                      ></v-autocomplete>


                    </v-col>
                    <v-col
                        cols="12"

                    >
                      <v-text-field
                          v-model="editedItem.PostCode"
                          label="PostCode"
                      ></v-text-field>
                    </v-col>
                    <v-col
                        cols="12"

                    >

                      <v-autocomplete
                          v-model="editedItem.AccommodationCity"
                          label="AccommodationCity "
                          :items="editedItem.AccommodationCities"
                          required
                          clearable
                          dense
                          reverse
                          filled

                      ></v-autocomplete>

                    </v-col>
                    <v-col
                        cols="12"
                    >
                      <v-text-field
                          v-model="editedItem.AccommodationAddress"
                          label="AccommodationAddress"
                      ></v-text-field>
                    </v-col>
                    <v-col
                        cols="12"
                    >
                      <v-text-field
                          v-model="editedItem.AccommodationTelephone"
                          label="AccommodationTelephone"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>



              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="blue darken-1"
                    text
                    @click="close"
                >
                  Cancel
                </v-btn>
                <v-btn
                    color="blue darken-1"
                    text
                    @click="save"
                >
                  Save
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="headline">از پاک کردن این آدرس مطمئن هستید؟</v-card-title>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete">خیر</v-btn>
                <v-btn color="blue darken-1" text @click="deleteItemConfirm">بله</v-btn>
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon
            small
            class="mr-2"
            @click="editItem(item)"
        >
          mdi-pencil
        </v-icon>
        <v-icon
            small
            @click="deleteItem(item)"
        >
          mdi-delete
        </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn
            color="primary"
            @click="initialize"
        >
          Reset
        </v-btn>
      </template>
    </v-data-table>
    </v-col>
    </v-row>
  </form>
</div>
</template>

<script>
export default {
  props: { 
    section: {
      type: String,
      required: true,
      default: () => null
    } 
  },
  data: () => ({
    date: "",
    files: null,
    party: {},
    Party: {
      name: "",
      Lname: "",
      BirthDate: null,
      IdNo: null,
      NationalID: null,
      BirthCity: null,
      FatherName: null,
      IssuanceCity: null,
      IssuanceDate: null,
      Gender: null,
      Genders: ["زن", "مرد"],
      Prefix: null,
      Prefixes: ["جناب آقای", "سرکار خانم"],
      location: null,
      start: null,
      end: null,
      email: "",
      nation: null,
      nations: [
        "ایرانی",
        "افغانستانی",
        "ارمنستانی",
        "ترک",
        "پاکستانی",
        "عراقی",
      ],
      Religion: null,
      Religions: ["اسلام", "مسیحیت", "یهودیت", "زرتشتی"],
      LivingCity: null,
      select: null,
      cities: ["تهران", "تبریز", "شیراز", "همدان"],
      checkbox: false,
      Role: [],
      Roles: [
        "کارشناس ",
        "بیمه‌گر اتکایی",
        "مرکز درمانی",
        "بازاریاب",
        "ذینفع",
        "بیمه شده",
        "بیمه گذار",
        "نماینده/شعبه",
      ],
      RetirementDate: null,
      PassportNo: "",
      PassportExpiryDate: null,
      ChildrenNo: null,
      Degree: null,
      Degrees: ["دکتری", "فوق لیسانس", "لیسانس", "فوق دیپلم", "دیپلم"],
      Job: null,
      Jobs: [],
      CommunicationWays: ["موبایل", "تلفن", "شبکه اجتماعی", "ایمیل"],
      CommunicateWay: [],
      CommunicateData: {}
    },
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: 'AddressType',
        align: 'start',
        sortable: false,
        value: 'AddressType',
      },
      { text: 'PostCode', value: 'PostCode' , sortable: false},
      { text: 'AccommodationCity', value: 'AccommodationCity' , sortable: false},
      { text: 'AccommodationAddress', value: 'AccommodationAddress' , sortable: false},
      { text: 'AccommodationTelephone', value: 'AccommodationTelephone', sortable: false },
      { text: 'Actions', value: 'actions', sortable: false },
    ],
    Parties: [],
    editedIndex: -1,
    editedItem: {
      AddressType: '',
      AddressTypes: ["محل کار", "محل زندگی"],
      PostCode: '',
      AccommodationCity: null,
      AccommodationCities: ["تهران", "تبریز", "شیراز", "همدان"],
      AccommodationAddress: '',
      AccommodationTelephone: '',
    },
    defaultItem: {
      AddressType: '',
      PostCode: 0,
      AccommodationCity: 0,
      AccommodationAddress: 0,
      AccommodationTelephone: 0,
    },
  }),
  watch: {
    dialog (val) {
      val || this.close()
    },
    dialogDelete (val) {
      val || this.closeDelete()
    },
    created () {
      this.initialize()
    }
  },
  computed: {
    validateEmail() {
      // eslint-disable-next-line no-useless-escape
      return /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(this.email)
    }
  },
  methods: {
    inputType(type) {
      let InputType = "";
      switch(type) {
        case "ایمیل": 
          InputType = "email";
          break;
        case "شبکه اجتماعی":
          InputType = "text";
          break;
        default: 
          InputType = "number";
          break;
      }
      return InputType
    },
    validate () {
      this.$refs.form.validate()
    },
    initialize () {
      this.Parties = [
        {
          AddressType: 'محل زندگی',
          PostCode: 113121155,
          AccommodationCity: 'تهران',
          AccommodationAddress: 'خیابان ولیعصر - خیابان انقلاب - کوچه پشن ',
          AccommodationTelephone: '021-88848414',
        },
        {
          AddressType: 'محل کار',
          PostCode: 113121155,
          AccommodationCity: 'تهران',
          AccommodationAddress: 'خیابان ولیعصر - خیابان انقلاب - کوچه پشن ',
          AccommodationTelephone: '021-88848414',
        },
      ]
    },
    editItem (item) {
      this.editedIndex = this.Parties.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },
    deleteItem (item) {
      this.editedIndex = this.Parties.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialogDelete = true
    },
    deleteItemConfirm () {
      this.Parties.splice(this.editedIndex, 1)
      this.closeDelete()
    },
    close () {
      this.dialog = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },
    closeDelete () {
      this.dialogDelete = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },
    save () {
      if (this.editedIndex > -1) {
        Object.assign(this.Parties[this.editedIndex], this.editedItem)
      } else {
        this.Parties.push(this.editedItem)
      }
      this.close()
    },
  }
}
</script>