<script setup lang="ts">
import { ref, computed } from 'vue'

// import { retails } from '/@src/data/layouts/view-list-v2'
import { listings } from '/@src/data/layouts/view-list-v2/apollo_listings'

type TabId = 'active' | 'inactive'
const activeTab = ref<TabId>('active')
const filters = ref('')

const filteredData = computed(() => {
  return listings
})
</script>

<template>
  <div class="list-view-toolbar">
    <!-- <VField>
      <VControl icon="feather:search">
        <input
          v-model="filters"
          class="input custom-text-filter"
          placeholder="Search..."
        />
      </VControl>
    </VField> -->
    <div class="column is-6">
      <VField>
        <VControl>
          <Multiselect
            v-model="filters"
            placeholder="Location"
            :options="[
              'Africa',
              'Andhra Pradesh',
              'Arabian Gulf',
              'Argentina',
              'Bahamas',
              'Bahrain',
              'Balearic Islands',
              'Baltic',
              'Bay of Bengal',
              'Black Sea',
              'Borneo',
              'Brazil',
              'British Columbia',
              'British Isles',
              'California',
              'Campania',
              'Canada',
              'Caribbean',
              'Carolinas',
              'Cayman Islands',
              'Central America',
              'Chile',
              'Columbia Caribbean',
              'Columbia Pacific',
              'Corsica & Sardinia',
              'Croatia',
              'Cyprus',
              'East Asia',
              'East Coast South America',
              'East Coast United States',
              'East Italy',
              'East Mediterranean',
              'East Mexico',
              'East Yucatan',
              'Ecuador',
              'Far East Russia',
              'Far North Alaska',
              'Florida - East Coast',
              'Florida - West Coast',
              'Florida Keys',
              'French Riviera',
              'Galapagos Islands',
              'Georgia',
              'Great Lakes',
              'Greater Antilles',
              'Greece',
              'Greenland',
              'Guianas',
              'Gujarat',
              'Hudson Bay',
              'Iberia',
              'Iceland',
              'Indian Ocean',
              'Indonesia',
              'Iran',
              'Italian Riviera',
              'Japan',
              'Java',
              'Kalimantan',
              'Kerala',
              'Konkan',
              'Kuwait',
              'Lazio',
              'Leeward Antilles',
              'Leeward Islands',
              'Lesser Sunda Islands',
              'Macaronesia',
              'Madagascar',
              'Malaysia',
              'Maldives',
              'Malta',
              'Maluku Islands',
              'Melanasia',
              'Micronesia',
              'Middle Atlantic',
              'Middle East',
              'Montenegro',
              'Myanmar',
              'Netherlands',
              'New England',
              'New South Wales Australia',
              'New Zealand',
              'Newfoundland',
              'North Africa',
              'North China',
              'North East Africa',
              'North Korea',
              'North West Russia',
              'Northern Europe',
              'Northern France',
              'Northern Territory Australia',
              'Northwest Territories',
              'Nova Scotia',
              'Oceania',
              'Okhotsk',
              'Oman',
              'Pakistan',
              'Peru',
              'Philippines',
              'Polynesia',
              'Qatar',
              'Quebec',
              'Queensland Australia',
              'Russia',
              'Saudi Arabia East',
              'Saudi Arabia West',
              'Scandinavia',
              'Sea of Cortez',
              'Siberia',
              'Sicily & Aeolian Islands',
              'South Africa',
              'South Australia',
              'South Central Alaska',
              'South Central America',
              'South China',
              'South East Asia',
              'South Korea',
              'South of France',
              'South West Alaska',
              'Spain',
              'Sulawesi',
              'Sumatra',
              'Tamil Nadu',
              'Thailand',
              'Trinidad & Tobago',
              'Turkey',
              'Turks Caicos',
              'Tuscany',
              'United Arab Emirates',
              'Urals',
              'Uruguay',
              'Venezuela',
              'Vietnam',
              'West Australia',
              'West Coast South America',
              'West Coast United States',
              'West Indian Ocean',
              'West Mediterranean',
              'West Mexico',
              'West Yucatan',
              'Western Gulf',
              'Western New guinea',
              'Windward Islands',
              'Yemen',
            ]"
          />
        </VControl>
      </VField>
    </div>
    <div class="column is-2">
      <VField>
        <VControl>
          <Multiselect
            v-model="filters"
            placeholder="Length"
            :options="[
              '30-50 ft',
              '50-100 ft',
              '100-150 ft',
              '150-200 ft',
              '200-250 ft',
              '250-300 ft',
              '300+ ft',
            ]"
          />
        </VControl>
      </VField>
    </div>
    <div class="column is-2">
      <VField>
        <VControl>
          <Multiselect
            v-model="filters"
            placeholder="Type"
            :options="[
              'Sailboat',
              'Catamaran',
              'Houseboat',
              'Motorboat',
              'Motor yacht',
              'Power catamaran',
            ]"
          />
        </VControl>
      </VField>
    </div>

    <!-- <div class="tabs-inner">
      <div class="tabs">
        <ul>
          <li :class="[activeTab === 'active' && 'is-active']">
            <a
              tabindex="0"
              @keydown.space.prevent="activeTab = 'active'"
              @click="activeTab = 'active'"
              ><span>Active</span></a
            >
          </li>
          <li :class="[activeTab === 'inactive' && 'is-active']">
            <a
              tabindex="0"
              @keydown.space.prevent="activeTab = 'inactive'"
              @click="activeTab = 'inactive'"
              ><span>Inactive</span></a
            >
          </li>
          <li class="tab-naver"></li>
        </ul>
      </div>
    </div> -->
  </div>

  <div class="page-content-inner">
    <!--List-->
    <div class="list-view list-view-v2">
      <!--List Empty Search Placeholder -->
      <VPlaceholderPage
        :class="[filteredData.length !== 0 && 'is-hidden']"
        title="We couldn't find any matching results."
        subtitle="Too bad. Looks like we couldn't find any matching results for the
          search terms you've entered. Please try different search terms or
          criteria."
        larger
      >
        <template #image>
          <img
            class="light-image"
            src="/@src/assets/illustrations/placeholders/search-2.svg"
            alt=""
          />
          <img
            class="dark-image"
            src="/@src/assets/illustrations/placeholders/search-2-dark.svg"
            alt=""
          />
        </template>
      </VPlaceholderPage>

      <!--Active Tab-->
      <div
        id="active-items-tab"
        class="tab-content"
        :class="[activeTab === 'active' && 'is-active']"
      >
        <div class="list-view-inner">
          <TransitionGroup name="list-complete" tag="div">
            <div v-for="item in filteredData" :key="item.position" class="list-view-item">
              <div class="list-view-item-inner">
                <img :src="item.header_image" alt="" />
                <div class="meta-left">
                  <h3>
                    <span>{{ item.name }}</span>
                  </h3>

                  <p>
                    <i aria-hidden="true" class="iconify" data-icon="feather:map-pin"></i
                    >&nbsp;
                    <span>{{ item.operating_in }}</span>
                  </p>

                  <span>
                    <span>Length: {{ item.key_details.length }}</span>
                    <i aria-hidden="true" class="fas fa-circle icon-separator"></i>
                    <span>Sleeps: {{ item.key_details.sleeps }}</span>
                    <i aria-hidden="true" class="fas fa-circle icon-separator"></i>
                    <span>Bedrooms: {{ item.key_details.cabins }}</span>
                    <i aria-hidden="true" class="fas fa-circle icon-separator"></i>
                    <span>Cabins: {{ item.key_details.cabins }}</span>
                    <i aria-hidden="true" class="fas fa-circle icon-separator"></i>
                    <span>Built: {{ item.key_details.built }}</span>
                  </span>

                  <div class="icon-list">
                    <span>{{ item.key_details.price }} per week</span>
                  </div>
                </div>
                <div class="meta-right">
                  <div class="buttons">
                    <VButton light>More Info</VButton>
                    <VButton color="primary" raised>Book Now</VButton>
                  </div>
                </div>
              </div>
            </div>
          </TransitionGroup>
        </div>

        <VFlexPagination
          v-if="filteredData.length > 5"
          :item-per-page="10"
          :total-items="873"
          :current-page="42"
          :max-links-displayed="7"
        />
      </div>

      <!--Inactive Tab-->
      <div
        id="inactive-items-tab"
        class="tab-content"
        :class="[activeTab === 'inactive' && 'is-active']"
      >
        <div class="list-view-inner">
          <!--Empty placeholder-->
          <VPlaceholderPage
            title="There are no inactive properties."
            subtitle="Looks like there are no inactive properties to display. You can
                disable and also enable a property from the property settings."
            larger
          >
            <template #image>
              <img
                class="light-image"
                src="/@src/assets/illustrations/placeholders/having-coffee.svg"
                alt=""
              />
              <img
                class="dark-image"
                src="/@src/assets/illustrations/placeholders/having-coffee-dark.svg"
                alt=""
              />
            </template>
          </VPlaceholderPage>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import '../../../../scss/abstracts/mixins';

.list-view-v2 {
  .list-view-item {
    @include vuero-s-card;

    margin-bottom: 16px;
    padding: 16px;

    &:hover,
    &:focus {
      box-shadow: var(--light-box-shadow);
    }

    .list-view-item-inner {
      display: flex;

      > img {
        display: block;
        min-height: 130px;
        max-height: 130px;
        min-width: 190px;
        max-width: 190px;
        object-fit: cover;
        border-radius: var(--radius);
      }

      .meta-left {
        display: flex;
        flex-direction: column;
        margin-left: 16px;

        h3 {
          font-family: var(--font-alt);
          color: var(--dark-text);
          font-weight: 600;
          font-size: 1.1rem;
          line-height: 1.5;

          .rating {
            margin-left: 12px;

            i {
              position: relative;
              top: -2px;
              font-size: 12px;
              color: var(--fade-grey-dark-4);

              &.active {
                color: #ffc43b;
              }
            }
          }
        }

        p {
          font-size: 0.95rem;
          color: var(--light-text);

          svg {
            height: 12px;
            width: 12px;
          }
        }

        > span {
          display: flex;
          align-items: center;
          margin-top: 10px;
          font-family: var(--font);
          font-size: 0.9rem;
          color: var(--primary);

          .icon-separator {
            font-size: 5px;
            color: var(--light-text);
            padding: 0 10px;
          }
        }

        .icon-list {
          margin-top: auto;
          display: flex;

          > span {
            display: flex;
            align-items: center;
            margin-right: 15px;

            span {
              font-size: 0.85rem;
              font-family: var(--font-alt);
              color: var(--dark-text);
            }

            i {
              font-size: 1.2rem;
              margin-right: 6px;
              color: var(--light-text);
            }
          }
        }
      }

      .meta-right {
        margin-left: auto;
        display: flex;
        align-items: center;
        justify-content: flex-end;

        .buttons {
          margin-bottom: 0;
          margin-right: 10px;
        }
      }
    }
  }
}

.is-dark {
  .list-view-v2 {
    .list-view-item {
      @include vuero-card--dark;

      .list-view-item-inner {
        .meta-left {
          h3 {
            color: var(--dark-dark-text) !important;

            .rating {
              i:not(.active) {
                color: var(--dark-sidebar-dark-2);
              }
            }
          }

          > span {
            color: var(--primary);
          }

          .icon-list {
            > span {
              span {
                color: var(--dark-dark-text);
              }
            }
          }
        }

        .meta-right {
          .buttons {
            .button {
              &:first-child {
                background: var(--dark-sidebar-light-2);
                border-color: var(--dark-sidebar-light-8);
                color: var(--dark-dark-text);
              }
            }
          }
        }
      }
    }
  }
}

@media only screen and (max-width: 767px) {
  .list-view-v2 {
    .list-view-item {
      padding: 20px;

      .list-view-item-inner {
        flex-direction: column;

        > img {
          width: 100%;
          max-width: 100%;
          min-height: 160px;
          max-height: 160px;
          margin-bottom: 1rem;
        }

        .meta-left {
          margin-left: 0;

          > span {
            margin-bottom: 16px;
          }

          .icon-list {
            flex-wrap: wrap;

            > span {
              flex-direction: column;
              text-align: center;
              margin: 10px;
              width: calc(33.3% - 20px);

              i {
                margin: 0;
              }
            }
          }
        }

        .meta-right {
          margin: 16px 0 0;

          .buttons {
            margin: 0;
            width: 100%;
            display: flex;
            justify-content: space-between;

            .button {
              width: 48%;
            }
          }
        }
      }
    }
  }
}

@media only screen and (min-width: 768px) and (max-width: 1024px) and (orientation: portrait) {
  .list-view-v2 {
    .list-view-inner {
      display: flex;
      flex-wrap: wrap;

      .list-view-item {
        padding: 20px;
        margin: 10px;
        width: calc(50% - 20px);

        .list-view-item-inner {
          flex-direction: column;
          height: 100%;
          min-height: 450px;

          > img {
            width: 100%;
            max-width: 100%;
            min-height: 160px;
            max-height: 160px;
            margin-bottom: 1rem;
          }

          .meta-left {
            margin-left: 0;

            > span {
              margin-bottom: 16px;
            }

            .icon-list {
              flex-wrap: wrap;

              > span {
                flex-direction: column;
                text-align: center;
                margin: 10px;
                width: calc(33.3% - 20px);

                i {
                  margin: 0;
                }
              }
            }
          }

          .meta-right {
            margin: auto 0 0;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;

            .buttons {
              margin: 16px 0 0;
              width: 100%;
              display: flex;
              justify-content: space-between;

              .button {
                width: 48%;
              }
            }
          }
        }
      }
    }
  }
}
</style>
