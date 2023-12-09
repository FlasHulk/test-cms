<template>
    <v-app id="inspire">
        <v-app-bar class="header">
            <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

            <v-btn class="balance">
                <v-icon>mdi-wallet-outline</v-icon>
                <span class="balance-text">Баланс</span>
                <p class="balance-price">30975 UAN</p>
            </v-btn>

            <v-btn class="settings" icon>
                <v-icon>mdi-cog-outline</v-icon>
            </v-btn>

            <v-btn
                    id="menu-activator"
                    class="language-switcher"
            >
                UA
            </v-btn>

            <v-menu activator="#menu-activator">
                <v-list>
                    <v-list-item
                            v-for="(item, index) in lang"
                            :key="index"
                            :value="index"
                    >
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

            <v-btn @click="toggleTheme" icon>
                <v-icon>mdi-theme-light-dark</v-icon>
            </v-btn>
        </v-app-bar>

        <v-main class="main">
            <v-navigation-drawer class="nav-bar" v-model="drawer">
                <div class="text-center nav-bar__avatar">
                    <v-avatar
                            color="blue"
                            icon="$vuetify"
                            image="@/assets/avatar.png"
                            size="80"
                    >
                    </v-avatar>
                    <h3>{{ user.name }}</h3>
                </div>


                <v-list nav>
                    <v-list-item
                            v-for="link in navBarLinks"
                            :key="link.value"
                            :prepend-icon="link.icn"
                            :title="link.title"
                            :value="link.value"
                    >
                    </v-list-item>
                </v-list>
            </v-navigation-drawer>

            <v-container class="container">

                <h1>Створити компанію</h1>

                <v-container>
                    <v-row>
                        <v-col class="create-company">
                            <v-sheet rounded="lg">
                                <v-expansion-panels multiple>
                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Місто
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-select
                                                    v-model="companyCreate.city"
                                                    variant="underlined"
                                                    :items="['California', 'Colorado', 'Florida', 'Georgia', 'Texas', 'Wyoming']"
                                            ></v-select>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Назва кампанії
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-text-field
                                                    v-model="companyCreate.name"
                                                    variant="underlined"
                                                    prepend-icon="mdi-alphabetical"
                                            ></v-text-field>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Категорія
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-select
                                                    v-model="companyCreate.category"
                                                    variant="underlined"
                                                    :items="['California', 'Colorado', 'Florida', 'Georgia', 'Texas', 'Wyoming']"
                                            ></v-select>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Бюджет кампанії
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-text-field
                                                    v-model="companyCreate.campaignBudget"
                                                    variant="outlined"
                                                    type="number"
                                                    hide-details
                                                    placeholder="Ведіть значення "
                                            >
                                            </v-text-field>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Бюджет на добу
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-text-field
                                                    v-model="companyCreate.budgetPerDay"
                                                    variant="outlined"
                                                    type="number"
                                                    hide-details
                                                    placeholder="Ведіть значення "
                                            >
                                            </v-text-field>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel class="broadcast-period">
                                        <v-expansion-panel-title>
                                            Період трансляції
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-text-field
                                                    variant="underlined"
                                                    type="date"
                                                    prepend-icon="mdi-calendar-text-outline"
                                                    v-model="companyCreate.broadcastPeriod"
                                            ></v-text-field>

                                            <v-chip-group class="broadcast-period__week" v-model="companyCreate.week" multiple>
                                                <v-chip value="НЕД">НЕД</v-chip>

                                                <v-chip value="ПОН">ПОН</v-chip>

                                                <v-chip value="ВІВ">ВІВ</v-chip>

                                                <v-chip value="СЕР">СЕР</v-chip>

                                                <v-chip value="ЧЕТ">ЧЕТ</v-chip>

                                                <v-chip value="ПʼЯ">ПʼЯ</v-chip>

                                                <v-chip value="СУБ">СУБ</v-chip>
                                            </v-chip-group>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel class="broadcast-period-time">
                                        <v-expansion-panel-title>
                                            Трансляція в період (з - до)
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <div class="broadcast-period-time--wrap">
                                                <v-text-field
                                                        v-model="companyCreate.broadcastPeriodFrom"
                                                        type="time"
                                                        variant="underlined"
                                                        prepend-icon="mdi-clock-outline"
                                                ></v-text-field>

                                                <v-text-field
                                                        v-model="companyCreate.broadcastPeriodTo"
                                                        type="time"
                                                        variant="underlined"
                                                        prepend-icon="mdi-clock-outline"
                                                ></v-text-field>
                                            </div>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Інтервал між показами
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-text-field
                                                    v-model="companyCreate.intervalBetweenReadings"
                                                    variant="outlined"
                                                    hide-details
                                                    placeholder="Ведіть значення "
                                            >
                                            </v-text-field>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel>
                                        <v-expansion-panel-title>
                                            Вибір оператора
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-select
                                                    v-model="companyCreate.operator"
                                                    variant="underlined"
                                                    :items="['California', 'Colorado', 'Florida', 'Georgia', 'Texas', 'Wyoming']"
                                            ></v-select>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel class="inventory">
                                        <v-expansion-panel-title>
                                            Inventory side filters
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-chip-group class="inventory__types" v-model="companyCreate.inventory">
                                                <v-chip value="A">A</v-chip>
                                                <v-chip value="B">B</v-chip>
                                            </v-chip-group>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>

                                    <v-expansion-panel class="dooh">
                                        <v-expansion-panel-title>
                                            Filter by DOOH inventory
                                        </v-expansion-panel-title>
                                        <v-expansion-panel-text>
                                            <v-item-group class="dooh-list" v-model="companyCreate.dooh">
                                                <v-item
                                                        v-for="n in 6"
                                                        :key="n"
                                                        :value="n"
                                                        v-slot="{ isSelected, toggle }"
                                                >
                                                    <v-card
                                                            :color="isSelected ? 'primary' : ''"
                                                            class="dooh-item"
                                                            @click="toggle"
                                                    >
                                                        <img :src="'/_nuxt/assets/dooh-item'+ n +'.png'" alt="img">
                                                    </v-card>
                                                </v-item>
                                            </v-item-group>
                                        </v-expansion-panel-text>
                                    </v-expansion-panel>
                                </v-expansion-panels>
                            </v-sheet>
                        </v-col>

                        <v-col>
                            <div class="company-map">
                                <div class="company-map__img">
                                    <img src="@/assets/map.png" alt="map">
                                </div>
                            </div>

                            <v-sheet class="company-select">
                                <p>Обрано: 7 од.</p>

                                <p>OST: 854201</p>

                                <div class="company-select__group-btn">
                                    <v-btn class="btn-see-all">Показати всі обрані</v-btn>

                                    <v-btn class="btn-confirm">Підтвердити</v-btn>

                                    <v-btn class="btn-delete-all"> Видалити всі</v-btn>
                                </div>

                            </v-sheet>

                            <div class="company-list">
                                <v-sheet v-for="company in companyList" :key="company.id">
                                    <v-card class="company">
                                        <v-card-item class="company-wrap">
                                            <div class="company-head">
                                                <p class="company-code">
                                                    Code {{ company.code }}
                                                </p>

                                                <div class="company-inventory">
                                                    {{ company.inventory }}
                                                </div>

                                                <p class="company-ost">
                                                    OST {{ company.ost }}
                                                </p>
                                            </div>

                                            <p class="company-type">
                                                {{ company.type }}
                                            </p>

                                            <p class="company-address">
                                                {{ company.address }}
                                            </p>
                                        </v-card-item>

                                        <v-card-actions class="company-delete">
                                            <v-btn @click="deleteCompany(company.id)" icon>
                                                <v-icon>mdi-delete-outline</v-icon>
                                            </v-btn>
                                        </v-card-actions>
                                    </v-card>
                                </v-sheet>
                            </div>
                        </v-col>
                    </v-row>
                </v-container>

            </v-container>
        </v-main>
    </v-app>
</template>

<script setup>
import {ref} from 'vue'
import {useTheme} from 'vuetify'

const theme = useTheme();
const drawer = ref(true);
const lang = ref([
    {title: 'UA'},
    {title: 'ENG'},
    {title: 'POL'},
]);
const navBarLinks = ref([
    {
        title: 'Дашборд',
        value: 'dashboard',
        icn: 'mdi-view-dashboard'
    },
    {
        title: 'Створити кампанію',
        value: 'create-campaign',
        icn: 'mdi-monitor-dashboard'
    },
    {
        title: 'Креативи',
        value: 'creative',
        icn: 'mdi-multimedia'
    },
    {
        title: 'Створені кампанії',
        value: 'created-campaigns',
        icn: 'mdi-format-list-bulleted'
    },
    {
        title: 'Аудиторія',
        value: 'audience',
        icn: 'mdi-google-classroom'
    },
    {
        title: 'Звітність',
        value: 'reporting',
        icn: 'mdi-chart-bar-stacked'
    },
]);
const user = ref({
    name: 'Користувач',
    img: '/public/favicon.icon',
});
const companyCreate = ref({
    city: '',
    name: '',
    category: '',
    campaignBudget: '',
    budgetPerDay: '',
    broadcastPeriod: '',
    week: [],
    broadcastPeriodFrom: '',
    broadcastPeriodTo: '',
    intervalBetweenReadings: '',
    operator: '',
    inventory: [],
    dooh: '',
});
let companyList = ref([
    {
        id: 1,
        code: '237a',
        inventory: 'A',
        ost: 5493,
        type: 'Octagon Digital Board 3x6',
        address: 'Київ, вул. Старовокзальная, 107'
    },
    {
        id: 2,
        code: '234a',
        inventory: 'B',
        ost: 54933,
        type: 'Octagon Digital Board 3x6',
        address: 'Київ, вул. Старовокзальная, 108'
    },
    {
        id: 3,
        code: '534a',
        inventory: 'B',
        ost: 54933,
        type: 'Octagon Digital Board 16x9',
        address: 'Київ, вул. Старовокзальная, 509'
    },
    {
        id: 4,
        code: '237a',
        inventory: 'A',
        ost: 5493,
        type: 'Octagon Digital Board 3x6',
        address: 'Київ, вул. Старовокзальная, 107'
    },
    {
        id: 5,
        code: '234a',
        inventory: 'B',
        ost: 54933,
        type: 'Octagon Digital Board 3x6',
        address: 'Київ, вул. Старовокзальная, 108'
    },
    {
        id: 6,
        code: '534a',
        inventory: 'B',
        ost: 54933,
        type: 'Octagon Digital Board 16x9',
        address: 'Київ, вул. Старовокзальная, 509'
    },
])

function toggleTheme() {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark';
}

function deleteCompany(id) {
    companyList.value = companyList.value.filter(item => item.id !== id)
}

</script>

<style scoped lang="scss">
.header {

  .v-btn {
    text-transform: unset;
    letter-spacing: unset;
  }

  .balance {
    margin-left: auto;

    .balance-text {
      padding: 0 5px 0 8px;

      @media screen and (max-width: 600px) {
        display: none;
      }
    }

    .balance-price {
      @media screen and (max-width: 600px) {
        padding-left: 5px;
      }
    }
  }

  .settings {

  }

  .language-switcher {
    @media screen and (max-width: 600px) {
      padding-left: 5px;
      padding-right: 5px;
      min-width: unset;
    }
  }
}

.nav-bar {
  .nav-bar__avatar {
    padding: 58px;
  }
}

.v-theme--light {
  .main {
    background: #F3F3F3;
  }
}

.main {
  .v-container {
    max-width: 100%;
  }

  .v-col {
    @media screen and (max-width: 849px) {
      padding-left: 0;
      padding-right: 0;
    }
  }

  h1 {
    @media screen and (max-width: 600px) {
      font-size: 29px;
    }
  }

  .container {
    padding: 20px;

    @media screen and (max-width: 600px) {
      padding: 15px;
    }

    .create-company {
      flex: 0 1 410px;
      padding: 0 10px 0 0;

      @media screen and (max-width: 1440px) {
        flex: 0 1 300px;
      }

      @media screen and (max-width: 849px) {
        flex: 1 1 auto;
        padding: 0;
      }

      .v-expansion-panels {
        .v-expansion-panel {
          &.v-expansion-panel--before-active,
          &.v-expansion-panel--after-active,
          &.v-expansion-panel--active {
            border-radius: 0;
            margin-top: 0;
          }

          .v-expansion-panel-title {
            .v-expansion-panel-title__icon {
              display: none;
            }

            &.v-expansion-panel-title--active {
              min-height: 48px;
            }
          }
        }

        .broadcast-period {
          .broadcast-period__week {
            gap: 1px;

            .v-chip {
              border-radius: 0;
              margin: 0;
              padding: 0 10px;
            }
          }
        }

        .broadcast-period-time {
          .broadcast-period-time--wrap {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 30px;

            @media screen and (max-width: 1365px) {
              grid-template-columns: 1fr;
              gap: 0;
            }
          }
        }

        .inventory {
          .inventory__types {
            .v-chip {
              border-radius: 0;
              padding: 0 10px;
            }
          }
        }
      }
    }

    .company-map {
      .company-map__img {
        img {
          width: 100%;
        }
      }
    }

    .company-select {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 15px;
      margin: 15px 0;
      padding: 20px;

      @media screen and (max-width: 1365px) {
        flex-wrap: wrap;
        justify-content: flex-start;
      }

      .company-select__group-btn {
        display: flex;
        align-items: center;
        gap: 15px;

        @media screen and (max-width: 1365px) {
          width: 100%;
        }

        @media screen and (max-width: 600px) {
          flex-direction: column;
        }

        .v-btn {
          text-transform: unset;
          letter-spacing: unset;

          @media screen and (max-width: 600px) {
            width: 100%;
          }

          &.btn-see-all,
          &.btn-confirm,
          &.btn-delete-all {
            border: 1px solid blue;
          }

          &.btn-see-all {
            color: blue;
          }

          &.btn-confirm {
            color: green;
          }

          &.btn-delete-all {
            color: red;
          }
        }
      }
    }

    .company-list {
      overflow-y: scroll;
      max-height: 400px;

      .v-sheet {
        &+.v-sheet {
          margin-top: 10px;
        }
      }

      .company {
        position: relative;

        .company-wrap {
          padding: 10px 65px 10px 10px;

          @media screen and (max-width: 600px) {
            padding: 10px 40px 10px 10px;
          }

          .company-head {
            display: flex;
            align-items: center;
            gap: 30px;
            margin-bottom: 15px;

            @media screen and (max-width: 600px) {
              flex-wrap: wrap;
              gap: 10px;
            }

            .company-inventory {
              border: 1px solid blue;
              display: flex;
              align-items: center;
              justify-content: center;
              width: 30px;
              height: 30px;
              padding: 5px;
              text-align: center;
              line-height: 100%;
            }

            .company-ost {
              color: grey;
            }
          }

          .company-type {
            margin-bottom: 15px;
            color: grey;
          }

          .company-address {}
        }

        .company-delete {
          position: absolute;
          top: 0;
          right: 0;

          button {
            @media screen and (max-width: 600px) {
              width: 30px;
              height: 30px;
            }
          }
        }
      }
    }

    .dooh {
      .dooh-list {
        display: flex;
        flex-wrap: wrap;
        gap: 5px;

        .dooh-item {
          padding: 5px;
          height: 100px;
          img {
            width: 100%;
            height: 100%;
          }
        }
      }
    }
  }
}

</style>