<template>
  <fs-wrapper-login-required>
    <fs-breadcrumbs>{{ $t('settings') }}</fs-breadcrumbs>
    <h1>{{ $t('settings') }}</h1>
    <div class="fs-content elevation-1 mt-5">
    <v-tabs v-model="active" color="primary" dark centered>
      <v-tab href="#settings">{{ $t('basics') }}</v-tab>
      <v-tab href='#avatar'>{{ $t('avatar') }}</v-tab>
      <v-tab href='#consent'>{{ $t('consent') }}</v-tab>
      <v-tab-item id="settings" class="fs-pad">
        <fs-table-account-settings />
      </v-tab-item>
      <v-tab-item id="avatar" class="fs-pad">
        <fs-avatar-uploader type="user" />
      </v-tab-item>
      <v-tab-item id="consent" class="fs-pad">
        <fs-consent-gdpr :intro="(true)" :profile="(true)" :model="(true)" />
      </v-tab-item>
    </v-tabs>
    </div>
  </fs-wrapper-login-required>
</template>

<script>
import FsWrapperLoginRequired from '~/components/stateless/FsWrapperLoginRequired'
import FsBreadcrumbs from '~/components/stateless/FsBreadcrumbs'
import FsTableAccountSettings from '~/components/stateful/FsTableAccountSettings'
import FsAvatarUploader from '~/components/stateful/FsAvatarUploader'
import FsConsentGdpr from '~/components/stateless/FsConsentGdpr'
export default {
  components: {
    FsWrapperLoginRequired,
    FsBreadcrumbs,
    FsTableAccountSettings,
    FsAvatarUploader,
    FsConsentGdpr,
  },
  layout: 'wide',
  data: function() {
    return {
      error: false,
      loading: true,
      active: 0
    }
  },
  methods: {
    bulkDelete: function() {
      this.deleting = true
      this.$fs.bulkDeleteDrafts()
      .then((result) => {
        (result) ? this.deleting = false : this.error = true
      })
      .catch((error) => { this.error = true })
    },
  }
}
</script>
