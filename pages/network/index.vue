<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <div>
    <v-row justify="center">
      <v-col :cols="12" class="elevation-4 mb-2 pa-0 ma-0">
        <v-breadcrumbs
          :items="breadcrumbItems"
          class="pa-2"
        >
          <template v-slot:item="{ item }">
            <v-breadcrumbs-item
              :nuxt="true"
              :to="item.to"
              :disabled="item.disabled"
              :exact="item.exact"
            >
              <img v-if="item.to == '/'" src="/favicon-16x16.png">
              {{ item.text }}
            </v-breadcrumbs-item>
          </template>

          <template v-slot:divider>
            <v-icon>mdi-chevron-right</v-icon>
          </template>
        </v-breadcrumbs>
      </v-col>
    </v-row>

    <v-row justify="center">
      <v-col
        v-for="item in assets"
        :key="item.name"
        :cols="12"
        :sm="4"
      >
        <v-card>
          <v-card-title>
            <h2 class="headline">
              {{ item.name }}
            </h2>
          </v-card-title>

          <v-card-text>
            <p>{{ item.text }}</p>
          </v-card-text>

          <v-list>
            <v-divider />

            <v-list-item-group>
              <v-list-item
                v-for="subitem in item.parts"
                :key="subitem.title"
                @click="trackEvent(subitem.url)"
              >
                <v-list-item-content>
                  <v-list-item-title>{{ subitem.title }}</v-list-item-title>
                </v-list-item-content>

                <v-list-item-action>
                  <v-icon>launch</v-icon>
                </v-list-item-action>
              </v-list-item>
            </v-list-item-group>
          </v-list>

          <v-card-actions />
        </v-card>
      </v-col>

      <v-col :cols="12">
        <v-card>
          <v-card-text>
            <h1 class="headline">
              Character Sheets for Wrath and Glory
            </h1>
            <p>
              Your currently will find fan-made character sheets. We will add and link to other
              resources like community pages, reference sheets and roleplaying hooks in the future.
              If you want to add your page assets or other stuff, reach out to via
              <a href="mailto:docsofdoom+network@gmail.com?subject=Network Request">docsofdoom+network(at)gmail.com</a>.
            </p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'Wrath & Glory Assets | Network',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Searching for fillable character sheets for Wrath and Glory? Then check out the '
            + 'network section for downloads and links to valuable stuff.',
        },
      ],
    };
  },
  data() {
    return {
      breadcrumbItems: [
        {
          text: '', nuxt: true, exact: true, to: '/',
        },
        {
          text: 'Network', nuxt: true, exact: true, to: '/network',
        },
      ],
      assets: [
        {
          name: 'Combat Cheat Sheet',
          type: 'Google Docs',
          author: 'u/Z_Scribe',
          text: 'Reddit user Z_Scribe created this three pages of reference sheet for combat, healing, dying, corruption and conditions.',
          parts: [
            { title: 'Combat Cheat Sheet' , url: 'https://docs.google.com/document/d/12VV1_0Zkcww3c7y_xYn2MBBO-xd7S4euskJWAnYcYh8/edit?usp=sharing' },
          ],
        },
        {
          name: 'Condensed Rules reference',
          type: 'MS Word on Google Drive',
          author: 'mikev37',
          text: 'mikev37 produced a condensed rules reference that helps the DM (and players) in their Wrath & Glory Campaigns.',
          parts: [
            { title: 'Condensed Rules', url: 'https://drive.google.com/file/d/0B9hL1gAseGFMeGFrWkZQa1d1T1AwaFhTSl9MbURFMldxcFQ0/view' },
          ],
        },
        {
          name: 'Form-Fillable Character Sheets',
          type: 'pdf',
          author: 'Deathbird',
          text: 'Deathbird has put on some quality fillable PDF character sheets for Wrath & Glory.',
          parts: [
            { title: 'Basis (non-psyker) sheet', url: 'https://drive.google.com/open?id=1_dcMhtBBCek_1MHEzYtJBGYtpTZoksGR' },
            { title: 'Psyker (One additional page) sheet', url: 'https://drive.google.com/open?id=1mDtQyRW_bT4kgno5Bz7WX1HlLYXikBqh' },
            { title: 'Psyker (Two additional pages) sheet', url: 'https://drive.google.com/open?id=1rs3aZH0M_SBZzGBv5tDeWUF1m5wvGtTS' },
            { title: 'Psychic Powers Only sheet', url: 'https://drive.google.com/open?id=1LlHLeGdb2h3DRd_qWAaroD07pEZzPDmB' },
          ],
        },
      ],
    };
  },
  methods: {
    trackEvent(url) {
      this.$ga.event('Outbound Asset Link', 'click', url, 10);
      window.open(url);
    },
  },
};
</script>
