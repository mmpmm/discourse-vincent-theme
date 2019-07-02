// functions  --------------------------------------------------------------------------------

// Calculate brightness value
@function brightness($color) {
  @return (red($color) + green($color) + blue($color)) / (255 * 3);
}

// to base color
@function brightness_ratio($base, $color) {
  @return abs(brightness($base) - brightness($color));
}

// Compare colors to higher contrast
@function contrast($base, $color1: white, $color2: black) {
  @return if(brightness_ratio($base, $color1) > brightness_ratio($base, $color2), $color1, $color2);
}

// Compare colors to lower contrast (inverting the former contrast function)
@function invert-contrast($base, $color1: white, $color2: black) {
  @return if(brightness_ratio($base, $color1) > brightness_ratio($base, $color2), $color2, $color1);
}

// reverse lightness
@function reverse-lightness($color) {
  $result: 0;
  $value: lightness($color);
  @if $value >= 50 {
    $result: scale-color($color, $lightness: -$value);
  } @else {
    $result: scale-color($color, $lightness: 100% - $value);
  }
  @return $result;
}

// Variables  ---------------------------------------------------------------------------------

/*
$primary
$secondary
$tertiary
$quaternary
$header_background
$header_primary
$highlight
$danger
$success
$love
*/

$n: none;
$i: !important;

// Basics -------------------------------

$v-font-weight: 300 !default;
$v-font-size: 1.2em !default;
$v-theme-background: url(#{$theme_background}) !default;
$v-hue: 0 !default;
$v-saturation: -20 !default;
$v-lightness: 0 !default;
$V-page-max-width: 90vw !default;

// palette colors -------------------------------

$theme-base: hsl(
    hue($tertiary) + $v-hue,
    saturation($tertiary) + $v-saturation,
    lightness($tertiary) + $v-lightness
  )
  !default;
$theme-trim: $quaternary !default;

$main-background: rgba($header_background, 0.9) !default;
$secondary-background: rgba($main-background, 0.5) !default;
$tertiary-background: rgba($main-background, 0.8) !default;
$text-base: reverse-lightness($secondary) !default;
$trim-background: rgba($text-base, 0.1) !default;
$border-color: desaturate($trim-background, 100%) !default;
$highlight-color: rgba($text-base, 0.25) !default;
$link-color: lighten($theme-base, 75%) !default;

// settings -------------------------------

$body-background-pattern-opacity: 0.25 !default;
$body-background-gradient-opacity: 0.95 !default;
$body-gradient-color-first: #1469B4;
$body-gradient-color-second: #1469B4; 
$highlight-speed: #{$highlight_duration}s !default;
$button-text-case: #{$button_text_case} !default;

// fonts --------------------------------------------------------------------------------------

html {
  font-family: "Assistant", sans-serif;
  background: #fff;
  font-size: 16px;
}

body,
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: $v-font-weight;
}

.cooked {
  font-size: $v-font-size;
  line-height: 1.65;
  letter-spacing: 0.3px;
  font-variant-ligatures: no-common-ligatures;
  -webkit-font-smoothing: subpixel-antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a {
  font-size: 90%;
}

.cooked {
  p,
  ul,
  ol {
    -webkit-text-stroke: 0.2px hsla(0, 0%, 50%, 1);
    color: #ffffff; 
    a {
      -webkit-text-stroke: 0;
    }
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    color: #ccc;
  }
}

.user-navigation .nav-stacked a.active {
  font-weight: normal;
}

#banner #banner-content span {
  text-decoration: none;
}

.main-content .nav-drop .selected-nav-item {
  line-height: 30px;
  height: 30px;
}

.user-badge,
#user-card.show-badges .more-user-badges {
  line-height: 19px;
}

i,
cite,
em,
var,
address,
dfn,
strong {
  font-size: 90%;
  -webkit-text-stroke: none;
}

#login-buttons button {
  font-size: 1em;
}

// Reset   ------------------------------------------------------------------------------------

.topic-list .posters,
input {
  box-sizing: content-box;
}

#topic-title .title-wrapper,
#topic-footer-buttons,
.embedded-posts.top,
#main-outlet,
.user-table {
  box-sizing: border-box;
}

body,
html {
  margin: 0;
  padding: 0;
}

* {
  outline-color: darken($theme-base, 15%) $i;
}

// colors -------------------------------------------------------------------------------------

// color text base -----------------------------

.badge-notification,
.category-list .topics .badge-notification,
.category-list .category .badge-notification,
.timeline-container .topic-timeline .timeline-handle,
.media .media-left img,
.modal-dialog .modal-content,
.modal-dialog.cascading-modal .modal-header,
.nav-pills > li.active > a,
.layouts-nav-button > li.active > a,
.nav-pills > li > a.active,
.layouts-nav-button > li > a.active,
.open .grippie,
.badge-notification.new-posts,
.badge-notification.unread-posts,
.admin-controls .nav.nav-pills li.active a,
#user-card .card-content,
.user-nav,
.badge-notification.clicks,
span.helpful-flags,
span.flagged-posts,
span.deleted-posts,
.modal.history-modal del,
.nav-stacked li a,
.timeline-container .topic-timeline .timeline-handle,
.media .media-left img,
.modal-dialog .modal-content,
.modal-dialog.cascading-modal .modal-header,
.nav-pills > li.active > a,
.layouts-nav-button > li.active > a,
.nav-pills > li > a.active,
.layouts-nav-button > li > a.active,
.open .grippie,
.badge-notification.new-posts,
.badge-notification.unread-posts,
.admin-controls .nav.nav-pills li.active a,
#reply-control.draft,
#reply-control.saving,
.topic-post.deleted .topic-meta-data span,
.topic-post.deleted .topic-meta-data a {
  color: $text-base;
}

.list-cell,
.table-heading,
.category-list td,
.category-list th,
.latest-topic-list .table-heading,
.settings .setting .desc,
#topic-footer-buttons p,
.small-action .small-action-desc.timegap,
.links-section .domain,
.top-sub-section .topic-info,
.user-main .staff-counters,
.topic-list .topic-list-item-separator td span,
nav.post-controls .highlight-action,
.gap,
.period-chooser .top-date-string,
.small-action .small-action-desc,
.small-action .topic-avatar i {
  color: darken($text-base, 40%);
}

// backgrounds --------------------------------------------------------------------------------

// background theme base -------------------------

.media .media-left img,
.modal-dialog .modal-content,
.modal-dialog.cascading-modal .modal-header,
.open .grippie,
.badge-notification.new-posts,
.badge-notification.unread-posts,
#reply-control.draft,
#reply-control.saving {
  background: green;
  color: contrast(mix($theme-base, $header_background, 75%));
}

// background main background  ------------------

.user-table,
.badge-card,
ul.general,
.boxed.white,
.alert.alert-info,
.body-page,
.topic-list,
.topic-list tbody tr:nth-of-type(even),
.category-list,
.category-list tbody tr:nth-of-type(even),
.search-container,
.search-advanced-options,
.user-stream-item.item,
tr.topic-list-item-separator + .topic-list-item + .topic-list-item,
.category-boxes .category-box-inner,
.category-boxes-with-topics .category-box-inner,
.list-controls,
.top-lists,
.topic-list-bottom,
.full-width > ul.nav.nav-pills,
#banner,
.latest-topic-list-item:nth-of-type(odd),
.latest-topic-list,
.offset2 .cooked,
#user-card .card-content,
.user-nav,
.user-main .staff-counters {
  background: $main-background;
  color: darken(desaturate(reverse-lightness($main-background), 100%), 50%);
}

.topic-meta-data,
.topic-map,
.reply .topic-meta-data,
.deleted section.embedded-posts .topic-meta-data {
  background: $tertiary-background;
  color: desaturate(reverse-lightness($tertiary-background), 100%);
}

// background secondary background --------------

.admin-controls,
section.embedded-posts {
  background: $secondary-background;
  color: desaturate(reverse-lightness($secondary-background), 100%);
}

// background custom background -----------------

.topic-post.deleted .topic-meta-data {
  background: rgba($danger, 0.8);
}

button.ok:hover {
  background: $success;
}

// background none ------------------------------

.nav-pills > li:not(.active) > a:hover,
.layouts-nav-button > li > a:hover,
.topic-body .reply-to-tab,
.list-controls a,
.d-header-icons a.icon,
.avatar-wrapper,
.user-navigation .nav-stacked a,
.user-content,
.main-content .nav-drop .nav-dropdown-menu a:hover,
.list-controls .category-dropdown-menu a:hover,
.list-controls .category-dropdown-menu a:hover,
.select-kit.combo-box.tag-drop .tag-drop-header,
.select-kit.combo-box.category-drop .category-drop-header,
li.toggle-maximize a,
a.mention,
a.mention-group,
.user-badge,
#user-card.show-badges .more-user-badges,
.list-controls .category-breadcrumb li.bullet > .dropdown-header,
.menu-links-header a:hover,
.extra-info-wrapper .discourse-tag,
.d-header-icons .icon:hover,
.d-header-icons .icon:active,
.widget-container,
tr.topic-list-item-separator + .topic-list-item,
.deleted .topic-body,
.topic-map .buttons .btn {
  background: $n;
}

// borders  ----------------------------------------------------------------------------------

// border border none ---------------------------

.main-content.nav-menu-enabled .list-controls,
div.menu-links-header a,
.user-main .about.collapsed-info .details,
.user-main .about .secondary,
.user-badge,
#user-card.show-badges .more-user-badges,
.d-editor-button-bar button,
.topic-list-item,
.topic-title,
.topic-post article.boxed,
.user-stream .item,
.user-stream .user-stream-item,
.d-header img.avatar,
.topic-status-info,
.main-content .list-controls,
.main-content.nav-menu-enabled .list-controls,
.main-content.has-sidebars .container.list-container,
img.avatar,
.topic-status-info,
.topic-avatar,
.topic-body,
.topic-map,
.topic-map section,
.embedded-posts .topic-body,
.embedded-posts .row,
.topic-map .buttons .btn,
.topic-post,
.select-kit.combo-box.tag-drop .tag-drop-header,
.select-kit.combo-box.category-drop .category-drop-header {
  border: $n $i;
}

// border border 1px  ----------------------------

.menu-panel,
#share-link.visible,
.admin-controls,
.user-stream .item,
.user-stream .user-stream-item,
#user-card .card-content,
#user-card.show-badges .badge-section .user-badge,
#user-card.show-badges .badge-section .more-user-badges,
.badge-card .badge-contents,
nav.post-controls .post-admin-menu,
.badges .content-list ul li {
  border: 1px solid;
}

// border border-top ------------------------------

hr,
.post-links-container .post-links,
.admin-contents table td,
.reply > .row,
.category-list tbody tr:first-of-type,
.reply .topic-body,
.small-action {
  border-top: 1px solid;
}

// border border-bottom ---------------------------

.topic-list .topic-list-item-separator td,
.nav-stacked li,
.admin-contents table td,
.table-heading,
.reply .topic-body {
  border-bottom: 1px solid;
}

// border border-color ----------------------------

img.avatar,
.menu-panel,
#share-link.visible,
.topic-list .topic-list-item-separator td,
.admin-controls,
.topic-status-info,
.admin-controls .nav.nav-pills li.active a,
hr,
.nav-stacked li,
.post-links-container .post-links,
.user-stream .item,
.user-stream .user-stream-item,
#user-card .card-content,
#user-card.show-badges .badge-section .user-badge,
#user-card.show-badges .badge-section .more-user-badges,
.badge-card .badge-contents,
nav.post-controls .post-admin-menu,
.badges .content-list ul li,
.admin-contents table td,
.reply,
.admin-list-item,
section.about table td,
section.about table th,
.display-row,
.search-advanced-options,
.user-stream-item.item,
.category-boxes .category-box-inner,
.category-boxes-with-topics .category-box-inner,
.category-list tbody tr,
.reply > .row,
.category-list tbody tr:first-of-type,
.reply .topic-body,
.small-action,
.category-list tbody tr,
.latest-topic-list-item,
.table-heading,
.reply .topic-body,
.topic-meta-data,
.latest-topic-list-item,
.category-list tbody tr,
.popup-menu {
  border-color: $border-color $i;
}

// border custom borders ---------------------------

img.avatar,
.docked .d-header {
  border-bottom: $n;
}

.drop-down-visible .d-header-icons .active .icon:after,
#reply-control.closed {
  border-top: $n;
}

.user-right .topic-list-item {
  border-right: $n;
}

.admin-detail {
  border-left: solid 1px $border-color;
}

.category-boxes .category-box-inner,
.category-boxes-with-topics .category-box-inner {
  border-width: 1px;
}

// Margins ------------------------------------------------------------------------------------

// 0 auto ------------------------------------------

.main-content,
img.avatar,
td.main-link .topic-thumbnail,
td.main-link .topic-title,
#topic-footer-buttons,
.main-content .regular,
#topic-title,
.alert,
#topic-title .title-wrapper,
#topic-footer-buttons {
  margin: 0 auto;
}

// margin zero --------------------------------------

.topic-list-item,
#list-area,
.topic-meta-data,
.extra-info-wrapper .topic-header-extra,
.show-more.has-topics .alert,
#post_1 .post-actions,
ol.category-breadcrumb {
  margin: 0;
}

// margin small all sides ---------------------------

.topic-avatar {
  margin: 0.5em;
}

// margin large all sides ---------------------------

.badges .content-list ul li,
.user-main .about .details img.avatar,
.user-main .about .details .primary h1,
.user-stream-item.item {
  margin: 1em;
}

// margin Large on side only ------------------------

.user-main .about .secondary dd,
.main-content {
  margin: 0 1em;
}

// up-down medium only ------------------------------

.top-title-buttons,
.user-stream .excerpt,
.alert,
.topic-post article.boxed,
.admin-controls {
  margin: 0.75em 0;
}

// up-down large only ------------------------------

.list-controls,
.top-lists,
.topic-list-bottom {
  margin: 1em 0;
}

// Top zero -----------------------------------------

.user-main .about.collapsed-info .details,
#user-card .user-card-avatar,
.top-lists,
.user-table,
.topic-map,
.embedded-posts .cooked,
.topic-body .regular,
section.post-menu-area,
.post-links-container .post-links {
  margin-top: 0;
}

// margin custom margin -----------------------------

.list-controls .btn,
.list-controls .nav,
section.post-menu-area {
  margin-bottom: 0;
}

.boxed.white {
  margin-bottom: 10em;
}

.desc {
  margin-top: 4px;
}

#user-card .user-card-avatar {
  margin-right: 0.5em;
}

.extra-info-wrapper .badge-wrapper.bullet {
  margin-top: 2px;
}

ul.subcat-list,
.topic-users {
  margin-left: 1em;
}

#reply-control #reply-title {
  margin-bottom: 10px;
}

.topic-map .avatar {
  margin-right: 4px;
}

.user-nav {
  margin: 10px 0;
}

.signup-cta .buttons,
.topic-area .presence-users {
  margin-bottom: 1em;
}

.topic-avatar,
.offset2 .topic-avatar {
  margin-left: 0;
  margin-top: 0;
}

.post-links-container ul li {
  margin-bottom: 0.5em;
}

.categories-list .category-list {
  margin-left: 0;
}

.cooked li {
  margin: 0.5em 0;
}

// padding ------------------------------------------------------------------------------------

// padding zero -------------------------------------

.topic-users > .inline,
a.mention,
a.mention-group,
.cooked .lightbox-wrapper,
.topic-post article.boxed,
.topic-avatar,
.topic-body,
.embedded-posts.bottom .row,
.boxed .contents,
.topic-post.deleted section.post-actions .post-action {
  padding: 0;
}

// Top zero -----------------------------------------

.topic-list-item,
.sidebar-container .sidebar-content > div,
.extra-info-wrapper .topic-header-extra {
  padding-top: 0;
}

// padding small all sides -------------------------

.topic-area .presence-users {
  padding: 0.5em;
}

// padding medium all sides -------------------------

.user-badge,
#user-card.show-badges .more-user-badges,
.topic-list-item,
.badge-info,
.top-lists,
.topic-list-bottom {
  padding: 0.75em;
}

// padding large all sides ---------------------------

.topic-list-item,
.user-stream .item,
.user-stream .user-stream-item,
.user-table,
.user-main .about.collapsed-info .details,
#user-card .card-content,
.body-page,
.search-container,
.search-advanced-options,
#topic-title .title-wrapper {
  padding: 1em;
}

// padding x-Large on sides only ----------------------

.topic-list .topic-list-item-separator td span,
.main-content .nav-drop .selected-nav-item,
.cooked,
.moderator .cooked,
.post-menu-area {
  padding: 0 1.25em;
}

// custom padding -------------------------------------

.post-links-container,
.reply .topic-body {
  padding: 0 1em;
}

.post-links-container ul li {
  padding: 0.25em;
}

.post-links-container .post-links {
  padding: 1em 0;
}

.topic-map .buttons .btn {
  padding: 3px 25px;
}

.sidebar-container .sidebar-content > div {
  padding-bottom: 0;
}
.content-wrapper {
  padding-bottom: 150px;
}

.user-right {
  padding-left: 1em;
}

.reply {
  padding-top: 1em;
}

.create-new-topic {
  padding: 5px 0px 0px 5px;
}
.list-controls .category-breadcrumb a.badge-category,
.list-controls .category-breadcrumb .dropdown-header {
  padding: 5px 8px 0 0;
}

nav.post-controls {
  padding: 0;
}

.admin-content .admin-contents,
.admin-detail {
  padding: 1.5em;
}

.boxed.white,
.user-table {
  padding-bottom: 3em;
}

.user-nav,
.full-width > ul.nav.nav-pills {
  padding-top: 10px;
  padding-bottom: 10px;
}

.reply .topic-body {
  padding-left: 0;
}

.topic-body .contents .cooked,
.offset2 .cooked {
  padding-top: 15px;
}

section.post-menu-area {
  padding: 10px;
}

section.embedded-posts.bottom,
section.embedded-posts.top {
  padding: 1em 0.5em 2em 0.5em;
}

.topic-post.deleted section.post-actions {
  padding: 0.5em;
}

#main-outlet {
  padding-top: 80px;
}

#post_1 .post-actions .post-action {
  padding: 0.25em 0;
  margin-top: 0;
}

.user-nav,
.full-width > ul.nav.nav-pills {
  padding: 10px;
}

.embedded-posts.top {
  padding-bottom: 1em $i;
}

a.expand-hidden {
  padding: 1.25em;
}

// Display and positioning --------------------------------------------------------------------

#topic-footer-buttons,
.top-title-buttons,
.user-badge,
#user-card.show-badges .more-user-badges,
.category-list tbody .category,
.nav-pills > li,
.layouts-nav-button > li {
  display: inline-block;
}

.user-main .about .secondary dd {
  display: inline;
}

.nav-pills > li,
.layouts-nav-button > li {
  float: none;
}

section.post-menu-area {
  position: relative;
}

.topic-avatar .avatar-flair {
  bottom: unset;
  top: 30px;
  right: -2px;
}

// height and width ---------------------------------------------------------------------------

// width 100% -----------------------------------------

.main-content .regular {
  width: 100%;
}

// max-width 95vw -------------------------------------

.main-content,
.alert,
#share-link.visible,
.wrap {
  max-width: $V-page-max-width;
}

// custom ---------------------------------------------

#topic-title .title-wrapper,
#topic-footer-buttons,
.topic-area .presence-users {
  max-width: 100%;
}

.embedded-posts.top {
  width: 890px;
}

.wrap {
  width: 90%;
}

#reply-control .d-editor-preview img:not(.thumbnail):not(.emoji),
.cooked img:not(.thumbnail):not(.emoji) {
  max-width: 100% $i;
  height: auto;
}

// Animation  ---------------------------------------------------------------------------------

.topic-list > tbody > tr.highlighted,
.topic-body.highlighted {
  animation: Vincent-highlight $highlight-speed ease-in-out;
}

@keyframes Vincent-highlight {
  0% {
    background-color: $highlight-color;
  }
}

// body background ----------------------------------------------------------------------------

body {
  position: relative;
  background-attachment: scroll;
  background-color: rgba(black, 0.1);
}

#background,
body:before {
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

body:before {
  display: block;
  content: "";
  width: 100vw;
  z-index: -2;
  opacity: $body-background-gradient-opacity;
  background: linear-gradient(
    to top left,
    $body-gradient-color-first,
    $body-gradient-color-second
  );
}

#background {
  background: url('https://s3.amazonaws.com/aws-website-wwwblockcollidercom-xzf3z/emb_nation_8bit.png');
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  width: 100%;
  /* Full height */
}

// fix IE EDGE backgrounds

@supports (-ms-ime-align: auto) {
  body:before {
    z-index: 1;
  }

  #background {
    z-index: 2;
  }

  #main {
    z-index: 4;
  }

  .fixed-modal {
    background: rgba(64, 64, 64, 0.83);
  }

  .bootbox.modal {
    box-shadow: 0 0 0 100vw rgba(0, 0, 0, 0.8);
  }

  .modal-backdrop {
    display: none;
  }
}

@supports (-ms-accelerator: true) {
  body:before {
    z-index: 1;
  }

  #background {
    z-index: 2;
  }

  #main {
    z-index: 4;
  }

  .fixed-modal {
    background: rgba(64, 64, 64, 0.83);
  }

  .bootbox.modal {
    box-shadow: 0 0 0 100vw rgba(0, 0, 0, 0.8);
  }

  .modal-backdrop {
    display: none;
  }
}

@media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
  body:before {
    z-index: 1;
  }

  #background {
    z-index: 2;
  }

  #main {
    z-index: 4;
  }

  .fixed-modal {
    background: rgba(64, 64, 64, 0.83);
  }

  .bootbox.modal {
    box-shadow: 0 0 0 100vw rgba(0, 0, 0, 0.8);
  }

  .modal-backdrop {
    display: none;
  }
}

// Links  -------------------------------------------------------------------------------------

a {
  text-decoration: underline;
  color: $link-color;
  transition: all 0.1s ease $i;

  &:visited,
  &:active,
  &.hashtag,
  &.hashtag:visited {
    color: $link-color;
  }
  &:hover {
    text-decoration: underline;
    color: invert-contrast($text-base) $i;
  }
  &.mention {
    color: adjust-hue($link-color, 10deg);
  }
  &.mention-group {
    color: adjust-hue($link-color, -10deg);
  }
}

.user-main .staff-counters a {
  color: $link-color;
}

// Buttons ------------------------------------------------------------------------------------

.btn {
  position: relative;
  text-transform: $button-text-case;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  transform: translate3d(0, 0, 0);
  color: invert-contrast($text-base);
  background-color: transparent;

  &:hover,
  &:focus {
    box-shadow: 0 5px 11px 0 rgba(0, 0, 0, 0.18),
      0 4px 15px 0 rgba(0, 0, 0, 0.15);
    transition: box-shadow 0.4s ease-out;
  }

  &:hover,
  &.btn-hover {
    background-color: darken($theme-base, 15%);
    color: $text-base;
  }

  &.btn-social:hover,
  &.btn-social.btn-hover {
    background-color: $border-color;
    color: $text-base;
  }

  &[href] {
    color: invert-contrast($text-base);
  }

  &:active,
  &.btn-active {
    background: lighten($theme-base, 15%);
  }

  &[disabled],
  &.disabled {
    opacity: 0.6;
  }

  &.hidden {
    display: none;
  }

  .d-icon {
    opacity: 0.9;

    &:hover {
      opacity: 1;
    }
  }

  &.btn-primary {
    color: $text-base;
    background-color: $border-color;

    &:hover,
    &.btn-hover {
      background-color: darken($theme-base, 15%);
      color: $text-base;
    }
  }

  &.btn-danger {
    color: $text-base;
    background-color: $danger;

    &:hover,
    &.btn-hover {
      background-color: lighten($danger, 15%);
      color: $text-base;
    }
  }
}

.d-editor-button-bar button {
  background-color: transparent;
  border: $n;
  box-shadow: $n;
  background: $n;
}

// Media queries ------------------------------------------------------------------------------

.topic-meta-data {
  padding: 0.75em;
  &:after {
    display: block;
    content: "";
    clear: both;
  }
}

@media (max-width: 660px) {
  .topic-avatar {
    margin-top: 1px;
  }
}

@media (max-width: 950px) {
  body {
    background: $n;
  }

  .topic-list th,
  .topic-list td {
    padding: 0.75em;
  }

  .topic-map {
    margin-bottom: 0;
  }
}

// Extras -------------------------------------------------------------------------------------

.pace .pace-progress {
  background: darken($theme-base, 15%);
}

.spinner {
  height: 35px;
  width: 35px;
  border: $n;
  box-shadow: inset 0 1px 1px lighten($theme-base, 15%);
  margin: 60px auto 0 auto;
}

.category-boxes .category-box-inner:hover,
.category-boxes-with-topics .category-box-inner:hover {
  background: $secondary-background;
  cursor: pointer;
}

.topic-list .posters a:first-child .avatar.latest:not(.single) {
  box-shadow: 0 0 2px 3px $link-color;
  top: 0;
}

.modal.history-modal .diff-ins {
  background: darken($theme-base, 15%);
}

.modal.history-modal ins {
  color: lighten($theme-base, 15%);
  background: darken($theme-base, 25%);
}

.read-state {
  right: 3px;
}

.badge-category-bg {
  border-radius: 100vw;
}

.badge-wrapper.box span.badge-category-bg {
  border-radius: 0;
}

header.d-header.clearfix {
  border-bottom: 1px solid green;
}

.menu-panel.drop-down {
  border-bottom: 1px solid green;
}

.modal-inner-container {
  background: $header_background;
}

aside.onebox header a[href] {
  color: darken($text-base, 30%);
}

aside.onebox .onebox-body a[href],
aside.onebox .onebox-body a[href]:visited {
  color: $link-color;
}

aside.onebox {
  border: none;
  border-left: 4px solid darken($text-base, 35%);
  background: $trim-background;
}

aside.quote .title,
aside.quote blockquote,
blockquote {
  border-left: 3px solid $theme-base;
  background-color: $trim-background;
}

.modal-backdrop {
  background-color: #222;
}

#banner {
  max-width: 95vw;
  box-sizing: border-box;
  margin: 0 auto;
}

.modal.history-modal span.edit-reason {
  background-color: $border-color;
}

.directory {
  background: $main-background;
  padding: 2em;
}

.directory table tr.me td {
  background: $border-color;
}

.bootbox.modal {
  .modal-footer {
    a.btn-primary {
      color: $text-base;
    }
  }
}

.show-more.has-topics .alert {
  background: lighten($main-background, 10%);
}

.topic-area .presence-users {
  background: transparent;
  border-bottom: 1px solid $border-color;
  width: auto;
  display: inline-block;
}

.timeline-container .topic-timeline .timeline-scrollarea {
  border-color: rgba(invert($header_background), 0.18);
}

// TESTS --------------------------------------------------------------------------------------

.container.show-badge {
  background: $main-background;
  padding: 2em;
  min-height: 70vh;
}

.list-controls .category-breadcrumb .dropdown-header {
  background: none $i;
  color: inherit $i;
}

.timeline-container .topic-timeline .timeline-handle {
  background: desaturate($theme-base, 20%);
}

.select-box-kit .select-box-kit-row.is-selected,
.select-box-kit .select-kit-row.is-selected,
.select-kit .select-box-kit-row.is-selected,
.select-kit .select-kit-row.is-selected {
  background: darken($theme-base, 25%);
}

.d-icon.d-icon-d-tracking,
.d-icon.d-icon-d-watching,
.badge-notification.new-topic {
  color: lighten(desaturate($theme-base, 20%), 10%);
}

table.topic-list > thead,
table.category-list > thead,
.latest-topic-list .table-heading,
.table-heading {
  background: $main-background;
  border-bottom: 1px solid $border-color;
}

.post-info .wiki,
.post-info .last-wiki-edit {
  color: $success $i;
}

.lazyYT.lazyYT-container {
  width: 890px;
  padding-bottom: calc(56.25% + 1.4em) $i;
  left: -1.25em $i;
}

span.badge-category-parent-bg {
  border-radius: 100vw 0 0 100vw;

  + .badge-category-bg {
    border-radius: 0 100vw 100vw 0;
    border-left: 1px solid $header_background;
  }
}

.groups-table,
.groups-table thead,
.groups-table tbody tr:nth-of-type(even) {
  background: $main-background;
}

.groups-table tr td,
.groups-table thead th {
  padding: 12px 5px $i;
}

.groups-table tr {
  border-bottom: $n;
}

.groups-table tr td.groups-info {
  padding-left: 10px $i;
}

.groups-table .groups-info span.group-avatar-flair {
  padding-right: 5px;
}

// plugin support -----------------------------------------------------------------------------

// Retort  ---------------------------------------------

button.post-retort {
  z-index: 1;
  float: none;
}

button.post-retort:first-of-type {
  margin-left: 1.25em;
}

// Whos online  ---------------------------------------

#whos-online {
  padding: 1em 0.75em;
  background: $main-background;
  margin-bottom: 1em;
}

// Discourse Spoiler Alert  ---------------------------

.spoiled p {
  text-shadow: inherit;
  -webkit-text-stroke: inherit;
  color: inherit;
}

// Discourse signature plugin  ------------------------

.user-signature {
  padding: 0 1.25em;
}

// Discourse assign plugin  ------------------------

p.assigned-to {
  padding: 0 1.25em;
}

// Inputs -----------------------------------------------------------------------------

$input-b0: #555 !default;
$input-b: darken($theme-base, 10%) !default;

input,
select,
textarea {
  transition: border-color ease 0.75s;

  &:focus:required:invalid:focus {
    box-shadow: 0 0 2px $danger;
  }
}

input {
  &[type="text"],
  &[type="password"],
  &[type="datetime"],
  &[type="datetime-local"],
  &[type="date"],
  &[type="month"],
  &[type="time"],
  &[type="week"],
  &[type="number"],
  &[type="email"],
  &[type="url"],
  &[type="search"],
  &[type="tel"],
  &[type="color"] {
    &:focus {
      border-color: $input-b0;
      border-bottom-color: $input-b;
      box-shadow: $n;
    }
  }
}

textarea {
  &:focus {
    border-color: $input-b0;
    border-bottom-color: $input-b;
    box-shadow: $n;
  }
}

// Select2 Combo-box  ----------------------

.select2-container-active {
  box-shadow: none;
}

.select2-drop-active {
  border-color: $input-b0;
  border-top-color: $input-b;
}

.select-box-kit,
.select-kit {
  &.combo-box {
    .select-box-kit-header,
    .select-kit-header {
      &.is-focused {
        border: 1px solid $input-b;
        -webkit-box-shadow: $n;
        box-shadow: $n;
      }
    }

    &.is-highlighted {
      .select-kit-header {
        border: 1px solid $input-b;
        -webkit-box-shadow: $n;
        box-shadow: $n;
      }
    }

    &.is-expanded {
      .select-kit-wrapper {
        border: 1px solid $input-b;
        -webkit-box-shadow: $n;
        box-shadow: $n;
      }
    }
  }
}

// Select2 legacy  ------------------------

.select2-container {
  &.select2-container-active {
    border-color: $input-b0;
    border-bottom-color: $input-b;
  }
}

.select2-dropdown-open a.select2-choice {
  border-color: $input-b0;
  border-bottom-color: $input-b;
}

.select2-drop-active {
  border: 1px solid $input-b;
  border-top: 0;
}

.select2-container-active {
  box-shadow: none;
}

// other inputs  --------------------------

.tag-chooser {
  &.select2-dropdown-open,
  &.select2-container-active {
    border-color: $input-b;
  }
}

.select2-container-multi
  .select2-choices
  .select2-search-field
  input.select2-active {
  background: none $i;
}

.select2-container-multi.select2-container-active .select2-choices {
  border-color: $input-b;
}

#reply-control .tag-chooser.select2-dropdown-open,
#reply-control .tag-chooser.select2-container-active {
  border-color: $input-b;
}

// date chooser navigation arrows
.pika-prev,
.pika-next {
  background-color: $input-b;
}

div.ac-wrap input[type="text"] {
  margin: 1px;
}

.select-kit.combo-box.category-drop .select-kit-body,
.select-kit.combo-box.tag-drop .select-kit-body {
  border: 1px solid $input-b0;
  box-shadow: none;
}

// groups  -------------------------------------------------------------------

.group {
  .group-details-container,
  .group-members,
  .group-members thead,
  .group-members tbody tr:nth-of-type(even),
  .group-logs thead,
  .group-logs tbody tr:nth-of-type(even),
  .group-activity.container,
  .group-post:nth-child(even),
  .group-logs,
  .group-edit,
  .group-logs-controls button {
    background: $main-background;
  }

  .group-nav li .active a,
  .group-nav li .active i {
    color: $header_primary;
  }

  .group-members thead th,
  .group-members tbody tr td,
  .group-logs thead th,
  .group-logs tbody tr td {
    padding: 12px 5px;
  }

  .group-members tr,
  .group-logs tr {
    border-bottom: $n;
  }

  table.group-members th {
    border-bottom: 1px solid #474747;
  }

  .group-members tr td:first-child,
  .group-members th:first-child,
  .group-logs tr td:first-child,
  .group-logs th:first-child {
    padding-left: 10px;
  }

  .group-info span.group-avatar-flair {
    padding-right: 5px;
  }

  .group-nav li a {
    color: inherit;
  }

  .group-activity.container {
    padding: 1em;
  }

  .group-activity-nav li a.active {
    background-color: #4b4b4b;
    font-weight: inherit;
  }

  .group-post {
    padding: 1em;
    border-bottom: 1px solid $border-color;
  }

  .group-edit {
    padding: 1em;
    border: $n;
  }

  .group-logs-controls button {
    margin: 1em 0;
    padding: 0.75em;
  }

  .group-members-input .ac-wrap {
    margin-top: 0.75em;
  }
}

// 404 page  -------------------------------------------------------------------

.page-not-found-topics {
  background: $main-background;
  padding: 1em;

  & + .row {
    background: $main-background;
    padding: 0 1em;
    margin-top: 1em;
  }
}

h1.page-not-found {
  margin: 0 0 20px 0;
}

// The pit  --------------------------------------------------------------------

.slick-initialized,
[dir] .slick-initialized {
  width: 890px;
  left: -1.25em $i;

  > p:empty {
    display: none;
  }
}

.list-controls #create-topic {
  opacity: 0.7;

  .d-icon {
    color: $theme-base;
  }

  &:hover,
  &.d-hover {
    opacity: 1;
    background: darken($theme-base, 15%);

    .d-icon {
      color: inherit;
    }
  }
}

.nav-pills > li > a {
  padding: 0px 12px;
}

.list-controls > .container {
  display: block;
  align-items: center;
}

section.post-actions:empty {
  display: $n;
}

.cooked {
  >  {
    .slick-initialized:first-child,
    .lazyYT-container:first-child {
      margin-top: -15px;
    }
  }
}

.popup-menu {
  background-color: $header_background;
  border-color: $border-color;
}

.d-header .menu-panel {
  box-shadow: $n;
  background-color: $header_background;
  border-top: 1px solid green;
}

.admin-contents.dashboard tbody {
  background: rgba(255, 255, 255, 0.1);
}

ul.nav.nav-pills {
  margin: 0.5em 0;
}

.admin-controls {
  padding-top: 0;
}

.nav-pills > li.active > a,
.admin-controls .nav.nav-pills li.active a:hover,
.layouts-nav-button > li.active > a,
.nav-pills > li > a.active,
.nav-pills > li > a.active:hover,
.layouts-nav-button > li > a.active,
.admin-controls .nav.nav-pills li.active a {
  background: none;
  color: #333;
}

.moderator .topic-body {
  border-left: 8px solid lighten(rgba(complement($theme-base), 0.65), 5%) $i;
}

.moderator .topic-meta-data {
  border-bottom: $n;
}

.moderator .topic-body .contents .cooked {
  background: $n;
  padding: 0 1.25em;
  padding-top: 15px;
}

section.navigation-container {
  width: 100%;
}

button {
  z-index: 1;
}

.admin-contents thead th {
  background: $header_background;
}

tbody {
  border-top-width: 1px;
}

// desktop only

html.desktop-view.not-mobile-device {
  .topic-post .row,
  .reply .topic-body {
    display: flex;
  }

  .reply .topic-body {
    flex-flow: column;
    flex: 1 0 auto;
  }

  section.navigation-container,
  .category-navigation {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
  }
  .list-controls .nav {
    flex: 1;
  }
  .topic-body {
    width: 890px;
    max-width: 890px;
  }
  .embedded-posts .topic-body {
    width: 100%;
  }
  #navigation-bar {
    margin: 0;
    span.unread {
      display: none;
    }
  }
}

// mobile only

html.mobile-view.mobile-device {
  .topic-avatar img.avatar {
    margin: 0;
  }

  .alert {
    margin-bottom: 1em $i;
  }

  section.post-actions {
    padding-top: 0.25em;
  }

  .post-action {
    margin-top: 0.25em;
    margin-left: 0.25em;
  }

  .post-actions {
    margin: 0;
    padding-bottom: 0.5em;
    display: flex;
    justify-content: flex-end;
    flex-direction: column;
    &:empty {
      display: none;
    }
  }

  @media (max-width: 400px) {
    #main-outlet {
      padding-right: 0;
      padding-left: 0;
    }

    .topic-meta-data {
      position: relative;
    }

    .topic-meta-data .post-info:not(.edits) {
      margin-right: 0;
    }

    .names .new_user a,
    .names .user-title,
    .names .user-title a {
      font-size: 90%;
    }

    .post-info.edits + a.reply-to-tab {
      bottom: 5px;
      right: 0.5em $i;
    }
  }

  // full width YT
  .mobile-device .lazyYT.lazyYT-container {
    max-width: 890px;
  }

  .list-controls .nav-pills > li {
    background: none;
    color: #ccc;
  }
  .list-controls .nav-pills {
    padding: 0 0.5em;
  }
}

.group-info .avatar-flair,
.groups-table .groups-info .avatar-flair {
  border-radius: 50%;
  align-items: center;
  justify-content: center;
  display: flex;
  i {
    font-size: 1.75em $i;
  }
}

.select-kit .select-kit-row.is-highlighted {
  background: rgba($theme-base, 0.35) $i;
}

// centered content

$q-background: rgba(contrast($text-base), 0.5) !default;

.cooked,
.post-menu-area,
.moderator .topic-body .contents .cooked {
  background: $header_background;
}

.mobile-view.mobile-device {
  .topic-post .boxed .contents {
    background: $header_background;
  }
}

.topic-avatar {
  width: unset;
  margin: 0;
  padding: 1em 0.5em 0 0.5em;
}

.topic-meta-data {
  padding: 0.5em;
  background: $q-background;
}

.topic-map {
  margin: 0;
  background: $q-background;
}

.post-stream {
  display: flex;
  align-items: center;
  flex-direction: column;
}

#topic-title .title-wrapper,
#topic-footer-buttons,
.small-action {
  max-width: 100%;
  background-color: #333;
}

#topic-title {
  padding: 0;
}

.time-gap {
  padding: 0 100px;
  margin-bottom: 0 !important;
}

.time-gap .topic-avatar {
  display: none;
}

//// --
.timeline-container {
  margin-left: 10%;

  @media all and (min-width: 10px) {
    margin-left: 10%;
  }
  @media all and (min-width: 10px) {
    margin-left: 10%;
  }
}

.topic-map .buttons .btn {
  box-shadow: none;
}

#topic-title {
  width: 890px;
  max-width: 100%;
}

#topic-title .title-wrapper {
  width: 890px;
}

#suggested-topics {
  width: 100%;
}

.topic-avatar .avatar-flair {
  top: 38px;
  right: 6px;
}

.topic-post {
  width: 100%;
  max-width: 890px;
}

.post-actions {
  background: $q-background;
  margin: 0;
  padding-bottom: 1em;
}

#topic-title h1 {
  width: 100%;
}

.small-action .topic-avatar {
  background: none;
}

.topic-avatar img.avatar {
  margin: 0;
}

.topic-meta-data .names {
  flex: 1 0 auto;
}

.topic-meta-data {
  display: flex;
  min-height: 46px;
  align-items: center;
}

.topic-avatar {
  padding: 9px 11px;
}

.topic-post {
  width: 100%;
}

.topic-meta-data .post-info {
  margin-right: 6px;
}

.topic-body .topic-meta-data {
  padding: 0.5em 0.5em 0.5em 66px;
}

.topic-post .topic-avatar {
  position: absolute;
}

.posts-wrapper {
  width: 890px;
  margin: 0 auto;
  max-width: 100%;
}

.gap {
  width: auto;
  padding: 1em;
}

#topic-title .title-wrapper {
  padding: 1em 0;
}

#topic-title .edit-topic-title {
  padding: 1em;
  background: rgba(0, 0, 0, 0.5);
}

#topic-title .title-wrapper {
  padding-bottom: 7px;
  margin-bottom: 16px;
}

.title-wrapper .topic-category {
  padding: 6px;
  align-items: center;
}

//
.embedded-posts {
  border: none;
}

.embedded-posts {
  margin-left: 0;
}

.embedded-posts .reply {
  margin-left: 30px;
}

.embedded-posts .topic-avatar {
  padding: 0.5em;
}

.reply .cooked {
  padding-bottom: 15px;
}

.embedded-posts.top {
  margin-left: 0;
}

.embedded-posts .collapse-down,
.embedded-posts .collapse-up {
  color: $text-base;
  background: $header_background;
  border-color: $border-color;
}
//

.timeline-container {
  z-index: -2;
}

.select-kit.dropdown-select-box .dropdown-select-box-header:hover .d-icon {
  color: inherit;
}

.list-controls {
  .btn {
    min-height: 36px;
  }
}

@if $dark_background_overlay == "true" {
  body:before {
    background: black;
    opacity: 0.6;
    z-index: 0;
  }

  #background {
    opacity: 0.65;
  }

  // fix IE EDGE backgrounds

  @supports (-ms-ime-align: auto) {
    body:before {
      z-index: 2;
    }

    #background {
      z-index: 1;
    }
  }

  @supports (-ms-accelerator: true) {
    body:before {
      z-index: 2;
    }

    #background {
      z-index: 1;
    }
  }

  @media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
    body:before {
      z-index: 2;
    }

    #background {
      z-index: 1;
    }
  }
}

#topic-title .title-wrapper {
  background: rgba(0, 0, 0, 0.5);
  padding: 1em;
  margin-top: 1em;
}

.post-links-container {
  background: rgba(0, 0, 0, 0.5);
}

.title-wrapper .topic-category {
  padding-left: 0;
}

.spoiled {
  -webkit-text-stroke: 0;
}

.category-title-link {
  text-decoration: none !important;
}

.fancy-title {
  text-decoration: none !important;
}

@if $rounded_borders == "true" {
  #post_1 .contents,
  .nav-pills > li.active > a,
  .topic-map .buttons .btn,
  #reply-control .d-editor-button-bar .btn {
    border-radius: 0;
  }

  .contents,
  .menu-panel.drop-down,
  .topic-map,
  .embedded-posts.bottom,
  article:not(#post_1) section.post-menu-area,
  .post-links-container,
  .reply .cooked {
    border-radius: 0 0 10px 10px;
  }

  .topic-meta-data,
  #reply-control,
  .embedded-posts.top {
    border-radius: 10px 10px 0 0;
  }

  .popup-menu,
  .list-controls,
  .select-kit.dropdown-select-box.is-expanded .select-kit-body,
  table,
  .column,
  .group-activity.container,
  #topic-title .title-wrapper,
  .row .alert.alert-info,
  .boxed.white,
  .cooked > blockquote,
  .topic-list-bottom,
  .group-details-container,
  .group-outlet,
  .admin-controls,
  #banner,
  .user-nav,
  .full-width > ul.nav.nav-pills,
  .list-controls button.btn,
  .moderator .topic-body,
  .topic-body.highlighted,
  #user-card {
    border-radius: 10px;
  }

  aside.quote {
    .title {
      border-radius: 10px 10px 0 0;
    }

    blockquote {
      border-radius: 0 0 10px 10px;
      color: #ccc;
    }
  }

  input[type],
  .btn,
  button:hover,
  button.d-hover {
    border-radius: 4px;
  }

  .topic-map .map-collapsed .buttons .btn {
    border-radius: 0 0 10px 0;
  }

  table,
  .column,
  .group-outlet,
  #user-card {
    overflow: hidden;
  }

  a {
    border-radius: 3px;
  }

  .cooked > .onebox,
  .user-table,
  .badge-card,
  .user-stream-item,
  .d-editor-preview blockquote,
  .d-editor-preview aside.onebox {
    border-radius: 10px;
  }

  .category-box,
  .category-box-inner {
    border-radius: 15px;
  }

  .embedded-posts.bottom {
    margin-top: -10px;
  }

  .post-actions {
    padding-top: 10px;
    margin-top: -10px;
  }

    .d-header .title {
        margin-top: 0;
    }

  // plugin support
  #whos-online {
    border-radius: 10px;
  }
}

.d-header #site-logo {
  padding-top: 5px;
  height: 60px;
}

.views.sortable.num, .num.views {
    display: none;
}
li.secondary {
    display: none;
}
