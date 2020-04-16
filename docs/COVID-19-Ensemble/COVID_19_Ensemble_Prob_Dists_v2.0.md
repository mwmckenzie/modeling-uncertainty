---
layout: default
title: Probability Distribution Creation
nav_order: 2
---

<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />
<title>COVID_19_Ensemble_Pickler_v2.0</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    color: #000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=1);
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
@media (max-width: 991px) {
  #ipython_notebook {
    margin-left: 10px;
  }
}
[dir="rtl"] #ipython_notebook {
  float: right !important;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#login_widget {
  float: right;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  text-align: center;
  vertical-align: middle;
  display: inline;
  opacity: 0;
  z-index: 2;
  width: 12ex;
  margin-right: -12ex;
}
.alternate_upload .btn-upload {
  height: 22px;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
[dir="rtl"] #tabs li {
  float: right;
}
ul#tabs {
  margin-bottom: 4px;
}
[dir="rtl"] ul#tabs {
  margin-right: 0px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons {
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-right {
  padding-top: 1px;
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-left {
  float: right !important;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: baseline;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
#tree-selector {
  padding-right: 0px;
}
[dir="rtl"] #tree-selector a {
  float: right;
}
#button-select-all {
  min-width: 50px;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
[dir="rtl"] #new-menu {
  text-align: right;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
[dir="rtl"] #running .col-sm-8 {
  float: right !important;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI colors. */
.ansibold {
  font-weight: bold;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  border-left-width: 1px;
  padding-left: 5px;
  background: linear-gradient(to right, transparent -40px, transparent 1px, transparent 1px, transparent 100%);
}
div.cell.jupyter-soft-selected {
  border-left-color: #90CAF9;
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected {
  border-color: #ababab;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 5px, transparent 5px, transparent 100%);
}
@media print {
  div.cell.selected {
    border-color: transparent;
  }
}
div.cell.selected.jupyter-soft-selected {
  border-left-width: 0;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 7px, #E3F2FD 7px, #E3F2FD 100%);
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #66BB6A -40px, #66BB6A 5px, transparent 5px, transparent 100%);
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  padding: 0.4em;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. We need the 0 value because of how we size */
  /* .CodeMirror-lines */
  padding: 0;
  border: 0;
  border-radius: 0;
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul {
  list-style: disc;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ul ul {
  list-style: square;
  margin: 0em 2em;
}
.rendered_html ul ul ul {
  list-style: circle;
  margin: 0em 2em;
}
.rendered_html ol {
  list-style: decimal;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
  margin: 0em 2em;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  background-color: #fff;
  color: #000;
  font-size: 100%;
  padding: 0px;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  border: 1px solid black;
  border-collapse: collapse;
  margin: 1em 2em;
}
.rendered_html td,
.rendered_html th {
  text-align: left;
  vertical-align: middle;
  padding: 4px;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget {
  float: right !important;
  float: right;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  margin-top: 6px;
}
span.save_widget span.filename {
  height: 1em;
  line-height: 1em;
  padding: 3px;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  display: none;
}
.command-shortcut:before {
  content: "(command)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Creating-and-Exporting-Probability-Distributions-for-the-Probabilistic-SEIR-Models">Creating and Exporting Probability Distributions for the Probabilistic SEIR Models<a class="anchor-link" href="#Creating-and-Exporting-Probability-Distributions-for-the-Probabilistic-SEIR-Models">&#182;</a></h1><p>Begin with library imports and a few various settings, as well as determining the overall population size for the probability distributions and SEIR models.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">from</span> <span class="nn">matplotlib.animation</span> <span class="k">import</span> <span class="n">FuncAnimation</span>
<span class="kn">import</span> <span class="nn">math</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">random</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">from</span> <span class="nn">scipy</span> <span class="k">import</span> <span class="n">stats</span>
<span class="kn">from</span> <span class="nn">scipy.stats</span> <span class="k">import</span> <span class="n">beta</span>
<span class="kn">import</span> <span class="nn">ipywidgets</span> <span class="k">as</span> <span class="nn">widgets</span>
<span class="kn">from</span> <span class="nn">IPython.display</span> <span class="k">import</span> <span class="n">display</span>
<span class="kn">import</span> <span class="nn">pickle</span>

<span class="n">sns</span><span class="o">.</span><span class="n">set</span><span class="p">()</span>
<span class="n">plt</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s2">&quot;figure.figsize&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mi">20</span><span class="p">,</span><span class="mi">10</span><span class="p">)</span>

<span class="o">%</span><span class="k">matplotlib</span> notebook

<span class="n">N</span> <span class="o">=</span> <span class="mi">10_000</span> <span class="c1"># population size</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="PERT-Probability-Distribution-Creation-Function">PERT Probability Distribution Creation Function<a class="anchor-link" href="#PERT-Probability-Distribution-Creation-Function">&#182;</a></h3><p>This function creates and returns a PERT beta distribution given expected mode/peak, min, and max values, as well as a sample size. Here we use the population size set above for all our created probability distributions. The shape of the PERT distribution can be altered with the temp value (lower value results in a flatter distribution - with 0 being a uniform distribution), which is defaulted to 4 if no value is provided.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">pert_dist</span><span class="p">(</span><span class="n">peak</span><span class="p">,</span> <span class="n">low</span><span class="p">,</span> <span class="n">high</span><span class="p">,</span> <span class="n">sample_size</span><span class="o">=</span><span class="n">N</span><span class="p">,</span> <span class="n">temp</span><span class="o">=</span><span class="mi">4</span><span class="p">):</span>
    
    <span class="n">pert</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="n">pert_loc</span> <span class="o">=</span> <span class="n">low</span>
    <span class="n">pert_scale</span> <span class="o">=</span> <span class="n">high</span> <span class="o">-</span> <span class="n">low</span>
    
    <span class="n">con_1</span> <span class="o">=</span> <span class="mi">1</span> <span class="o">+</span> <span class="n">temp</span> <span class="o">*</span> <span class="p">(</span><span class="n">peak</span> <span class="o">-</span> <span class="n">low</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">high</span> <span class="o">-</span> <span class="n">low</span><span class="p">)</span>
    <span class="n">con_0</span> <span class="o">=</span> <span class="mi">1</span> <span class="o">+</span> <span class="n">temp</span> <span class="o">*</span> <span class="p">(</span><span class="n">high</span> <span class="o">-</span> <span class="n">peak</span><span class="p">)</span> <span class="o">/</span> <span class="p">(</span><span class="n">high</span> <span class="o">-</span> <span class="n">low</span><span class="p">)</span>
    
    <span class="n">pert</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">random</span><span class="o">.</span><span class="n">beta</span><span class="p">(</span><span class="n">con_1</span><span class="p">,</span> <span class="n">con_0</span><span class="p">,</span> <span class="n">sample_size</span><span class="p">)</span>
    <span class="n">pert</span> <span class="o">=</span> <span class="n">pert_loc</span> <span class="o">+</span> <span class="n">pert_scale</span> <span class="o">*</span> <span class="n">pert</span>
    <span class="k">return</span> <span class="n">pert</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Finding-best-fit-PERT/beta-distributions-using-the-find_beta-function">Finding <em>best fit</em> PERT/beta distributions using the find_beta function<a class="anchor-link" href="#Finding-best-fit-PERT/beta-distributions-using-the-find_beta-function">&#182;</a></h3><p>Many - if not most - of the data we are working with for our models has estimated means and confidence intervals for low/high values. Wanting to use this information to create <em>best guess</em> distributions, we use the find_beta function created below to find a <em>best fit</em> PERT/beta distribution given the known estimates. Inputs to the function are the mean and low/high CI values.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">find_beta</span><span class="p">(</span><span class="n">exp_mu</span><span class="p">,</span> <span class="n">exp_low</span><span class="p">,</span> <span class="n">exp_high</span><span class="p">,</span> <span class="n">exp_lda</span><span class="o">=</span><span class="mi">4</span><span class="p">):</span>
    <span class="n">mu_range</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="n">exp_low</span><span class="p">,</span> <span class="n">exp_high</span><span class="p">,</span> <span class="mi">40</span><span class="p">)</span>
    <span class="n">low_range</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="n">exp_mu</span><span class="p">,</span> <span class="mi">40</span><span class="p">)</span>
    <span class="n">high_range</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">linspace</span><span class="p">(</span><span class="n">exp_mu</span><span class="p">,</span> <span class="p">(</span><span class="n">exp_high</span> <span class="o">*</span> <span class="mi">2</span><span class="p">),</span> <span class="mi">40</span><span class="p">)</span>
    <span class="n">test_res</span><span class="p">,</span> <span class="n">mu_res</span><span class="p">,</span> <span class="n">low_res</span><span class="p">,</span> <span class="n">high_res</span><span class="p">,</span> <span class="n">mean_err_rec</span><span class="p">,</span> <span class="n">exp_mu_rec</span> <span class="o">=</span> <span class="p">[],</span> <span class="p">[],</span> <span class="p">[],</span> <span class="p">[],</span> <span class="p">[],</span> <span class="p">[]</span>
    
    <span class="k">for</span> <span class="n">mu</span> <span class="ow">in</span> <span class="n">mu_range</span><span class="p">:</span>
        <span class="k">for</span> <span class="n">low</span> <span class="ow">in</span> <span class="n">low_range</span><span class="p">:</span>
            <span class="k">for</span> <span class="n">high</span> <span class="ow">in</span> <span class="n">high_range</span><span class="p">:</span>
                <span class="k">if</span> <span class="n">low</span> <span class="o">&gt;=</span> <span class="n">mu</span><span class="p">:</span>
                    <span class="n">low</span> <span class="o">=</span> <span class="n">mu</span> <span class="o">*</span> <span class="o">.</span><span class="mi">8</span>
                <span class="k">if</span> <span class="n">high</span> <span class="o">&lt;=</span> <span class="n">mu</span><span class="p">:</span>
                    <span class="n">high</span> <span class="o">=</span> <span class="n">mu</span> <span class="o">*</span> <span class="mf">1.2</span>
                <span class="n">test_dist</span> <span class="o">=</span> <span class="n">pert_dist</span><span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">low</span><span class="p">,</span> <span class="n">high</span><span class="p">,</span> <span class="mi">1000</span><span class="p">,</span> <span class="n">exp_lda</span><span class="p">)</span>
                <span class="n">test_mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">test_dist</span><span class="p">)</span>
                <span class="n">test_low</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">percentile</span><span class="p">(</span><span class="n">test_dist</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span>
                <span class="n">test_high</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">percentile</span><span class="p">(</span><span class="n">test_dist</span><span class="p">,</span> <span class="mi">90</span><span class="p">)</span>
                <span class="n">mean_err</span> <span class="o">=</span> <span class="p">(</span><span class="n">test_mean</span> <span class="o">-</span> <span class="n">exp_mu</span><span class="p">)</span><span class="o">**</span><span class="mi">2</span>
                <span class="n">low_err</span> <span class="o">=</span> <span class="p">(</span><span class="n">test_low</span> <span class="o">-</span> <span class="n">exp_low</span><span class="p">)</span><span class="o">**</span><span class="mi">2</span>
                <span class="n">high_err</span> <span class="o">=</span> <span class="p">(</span><span class="n">test_high</span> <span class="o">-</span> <span class="n">exp_high</span><span class="p">)</span><span class="o">**</span><span class="mi">2</span>
                <span class="n">test_res</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">mean_err</span> <span class="o">+</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">mean_err</span> <span class="o">+</span> <span class="n">low_err</span> <span class="o">+</span> <span class="n">high_err</span><span class="p">))</span>
                <span class="n">mu_res</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">mu</span><span class="p">)</span>
                <span class="n">low_res</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">low</span><span class="p">)</span>
                <span class="n">high_res</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">high</span><span class="p">)</span>
                <span class="n">mean_err_rec</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">mean_err</span><span class="p">))</span>
                <span class="n">exp_mu_rec</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">exp_mu</span><span class="p">)</span>
                
    <span class="n">full_results</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span>
        <span class="s1">&#39;Test Results&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">test_res</span><span class="p">),</span>
        <span class="s1">&#39;Mode Value&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">mu_res</span><span class="p">),</span>
        <span class="s1">&#39;Low Value&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">low_res</span><span class="p">),</span>
        <span class="s1">&#39;High Value&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">high_res</span><span class="p">),</span>
        <span class="s1">&#39;mean_err&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">mean_err_rec</span><span class="p">),</span>
        <span class="s1">&#39;expected mu&#39;</span><span class="p">:</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">exp_mu_rec</span><span class="p">)</span>
    <span class="p">})</span>
    <span class="k">return</span> <span class="n">full_results</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="The-df_dist-class">The df_dist class<a class="anchor-link" href="#The-df_dist-class">&#182;</a></h3><p>The df_dist class is created by providing the expected mean, low/high CI, distribution size, beta temperature (see above to explanation of beta temps), and a name. Only mean and low/high values are required, all others have a default. The class is created by finding a best fit PERT distribution that is then available as an attribute (df_dist.pert). The df_dist class also has a checkParams function that both provides an information display about desired and resulting mean/low/high CI values, as well as a histogram plot of the resulting probability distribution. Finally, the df_dist class has a getSample() method for returning a random sample from the instance's PERT/beta distribution.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">df_dist</span><span class="p">:</span>
    
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">dist_mu</span><span class="p">,</span> <span class="n">dist_low</span><span class="p">,</span> <span class="n">dist_high</span><span class="p">,</span> <span class="n">dist_size</span><span class="o">=</span><span class="mi">10_000</span><span class="p">,</span> <span class="n">dist_temp</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;Unknown&#39;</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">mu</span> <span class="o">=</span> <span class="n">dist_mu</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">low</span> <span class="o">=</span> <span class="n">dist_low</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">high</span> <span class="o">=</span> <span class="n">dist_high</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">temp</span> <span class="o">=</span> <span class="n">dist_temp</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">dsize</span> <span class="o">=</span> <span class="n">dist_size</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">name</span> <span class="o">=</span> <span class="n">name</span>
        
        <span class="bp">self</span><span class="o">.</span><span class="n">df</span> <span class="o">=</span> <span class="n">find_beta</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">mu</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">low</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">high</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">temp</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">df</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="p">[</span><span class="s1">&#39;Test Results&#39;</span><span class="p">],</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">new_mu</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">new_low</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">new_high</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">df</span><span class="o">.</span><span class="n">iloc</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">:</span><span class="mi">4</span><span class="p">])</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">pert</span> <span class="o">=</span> <span class="n">pert_dist</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">new_mu</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">new_low</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">new_high</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">dsize</span><span class="p">,</span> <span class="bp">self</span><span class="o">.</span><span class="n">temp</span><span class="p">)</span>
        
    <span class="k">def</span> <span class="nf">checkParams</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">f</span><span class="s1">&#39;Pert vars: mu: </span><span class="si">{self.new_mu}</span><span class="s1">, low: </span><span class="si">{self.new_low}</span><span class="s1">, high: </span><span class="si">{self.new_high}</span><span class="s1">&#39;</span><span class="p">)</span>
        
        <span class="n">plt</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">pert</span><span class="p">,</span> <span class="mi">25</span><span class="p">)</span>
        <span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
        
        <span class="nb">print</span><span class="p">(</span><span class="n">f</span><span class="s1">&#39;Original inputs: Mean=</span><span class="si">{self.mu}</span><span class="s1">, Low=</span><span class="si">{self.low}</span><span class="s1">, High=</span><span class="si">{self.high}</span><span class="s1">&#39;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">f</span><span class="s1">&#39;New outputs: Mean={np.mean(self.pert)}, Low={np.percentile(self.pert, 10)}, High={np.percentile(self.pert, 90)}&#39;</span><span class="p">)</span>

    <span class="k">def</span> <span class="nf">getSample</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="k">return</span> <span class="n">random</span><span class="o">.</span><span class="n">sample</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">pert</span><span class="p">),</span> <span class="mi">1</span><span class="p">)[</span><span class="mi">0</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Creating-the-probability-distributions-for-each-of-the-required-variables-for-a-probabilistic-SEIR-model">Creating the probability distributions for each of the required variables for a probabilistic SEIR model<a class="anchor-link" href="#Creating-the-probability-distributions-for-each-of-the-required-variables-for-a-probabilistic-SEIR-model">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># length of incubation period</span>
<span class="c1"># Defaults: mean 5.1, min CI value of 1.9, max CI value of 15.6</span>
<span class="n">e2i</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">(</span><span class="mf">5.1</span><span class="p">,</span> <span class="mf">2.5</span><span class="p">,</span> <span class="mf">11.5</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="s1">&#39;Incubation Period&#39;</span><span class="p">)</span>

<span class="c1"># spread mostly likely during infectious period, unlikely once recovery begins: https://www.statnews.com/2020/03/09/people-shed-high-levels-of-coronavirus-study-finds-but-most-are-likely-not-infectious-after-recovery-begins/</span>
<span class="c1"># infectious period, time to begining recovery after exposure to infectious transition</span>
<span class="c1"># Defaults: </span>
<span class="n">i2r</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">(</span><span class="mi">7</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">12</span><span class="p">,</span> <span class="n">N</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="s1">&#39;Infectious Period&#39;</span><span class="p">)</span>

<span class="c1"># (.009 default) case fatality rate, https://wwwnc.cdc.gov/eid/article/26/6/20-0320_article</span>
<span class="c1"># Defaults: mean .009, min CFR (.0025), max CFR (.03 default)</span>
<span class="n">cfr</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">(</span><span class="o">.</span><span class="mi">015</span><span class="p">,</span> <span class="o">.</span><span class="mi">0025</span><span class="p">,</span> <span class="o">.</span><span class="mi">03</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;Case Fatality Rate&#39;</span><span class="p">)</span>

<span class="c1"># H1N1 ratio for confirmed cases to estimated total infected</span>
<span class="n">c2i</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">((</span><span class="mi">1</span><span class="o">/</span><span class="mi">79</span><span class="p">),</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="mi">148</span><span class="p">),</span> <span class="p">(</span><span class="mi">1</span><span class="o">/</span><span class="mi">47</span><span class="p">),</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;Confirmed to Infectious Ratio&#39;</span><span class="p">)</span>

<span class="c1"># H1N1 ratio for hospitalized to infected</span>
<span class="n">h2i</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">(</span><span class="o">.</span><span class="mi">0045</span><span class="p">,</span> <span class="o">.</span><span class="mi">0016</span><span class="p">,</span> <span class="o">.</span><span class="mi">012</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;Hospitalized to Infectious Ratio&#39;</span><span class="p">)</span>

<span class="c1"># person-to-person spread: primary means of propagation https://www.cdc.gov/coronavirus/2019-ncov/prepare/transmission.html?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fabout%2Ftransmission.html</span>
<span class="n">freq_cont</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;Daily Frequent Contacts&#39;</span><span class="p">)</span>
<span class="n">infreq_cont</span> <span class="o">=</span> <span class="n">df_dist</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="n">name</span><span class="o">=</span><span class="s1">&#39;Daily Infrequent Contacts&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Exporting-the-distributions-for-later-import-and-usage">Exporting the distributions for later import and usage<a class="anchor-link" href="#Exporting-the-distributions-for-later-import-and-usage">&#182;</a></h3><p>Exporting the above distribution class objects for later use in a modified application in order to save time and computational energy by avoiding rerunning the intense distribution finding algorithms of the distribution classes.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;e2i_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">e2i</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;i2r_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">i2r</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">filename</span> <span class="o">=</span>  <span class="s1">&#39;c2i_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">c2i</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;h2i_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">h2i</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;freq_cont_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">freq_cont</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;infreq_cont_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">infreq_cont</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>

<span class="n">filename</span> <span class="o">=</span> <span class="s1">&#39;cfr_object&#39;</span>
<span class="n">outfile</span> <span class="o">=</span> <span class="nb">open</span><span class="p">(</span><span class="n">filename</span><span class="p">,</span> <span class="s1">&#39;wb&#39;</span><span class="p">)</span>
<span class="n">pickle</span><span class="o">.</span><span class="n">dump</span><span class="p">(</span><span class="n">cfr</span><span class="p">,</span> <span class="n">outfile</span><span class="p">)</span>
<span class="n">outfile</span><span class="o">.</span><span class="n">close</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Example-of-the-checkParams()-method-and-associated-output">Example of the checkParams() method and associated output<a class="anchor-link" href="#Example-of-the-checkParams()-method-and-associated-output">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">e2i</span><span class="o">.</span><span class="n">checkParams</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Pert vars: mu: 2.730769230769231, low: 0.6538461538461537, high: 23.0
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>





<div id="e7d8b86f-e2a5-430e-bd87-e544c7c974d4"></div>
<div class="output_subarea output_javascript ">
<script type="text/javascript">
var element = $('#e7d8b86f-e2a5-430e-bd87-e544c7c974d4');
/* Put everything inside the global mpl namespace */
window.mpl = {};


mpl.get_websocket_type = function() {
    if (typeof(WebSocket) !== 'undefined') {
        return WebSocket;
    } else if (typeof(MozWebSocket) !== 'undefined') {
        return MozWebSocket;
    } else {
        alert('Your browser does not have WebSocket support.' +
              'Please try Chrome, Safari or Firefox ≥ 6. ' +
              'Firefox 4 and 5 are also supported but you ' +
              'have to enable WebSockets in about:config.');
    };
}

mpl.figure = function(figure_id, websocket, ondownload, parent_element) {
    this.id = figure_id;

    this.ws = websocket;

    this.supports_binary = (this.ws.binaryType != undefined);

    if (!this.supports_binary) {
        var warnings = document.getElementById("mpl-warnings");
        if (warnings) {
            warnings.style.display = 'block';
            warnings.textContent = (
                "This browser does not support binary websocket messages. " +
                    "Performance may be slow.");
        }
    }

    this.imageObj = new Image();

    this.context = undefined;
    this.message = undefined;
    this.canvas = undefined;
    this.rubberband_canvas = undefined;
    this.rubberband_context = undefined;
    this.format_dropdown = undefined;

    this.image_mode = 'full';

    this.root = $('<div/>');
    this._root_extra_style(this.root)
    this.root.attr('style', 'display: inline-block');

    $(parent_element).append(this.root);

    this._init_header(this);
    this._init_canvas(this);
    this._init_toolbar(this);

    var fig = this;

    this.waiting = false;

    this.ws.onopen =  function () {
            fig.send_message("supports_binary", {value: fig.supports_binary});
            fig.send_message("send_image_mode", {});
            if (mpl.ratio != 1) {
                fig.send_message("set_dpi_ratio", {'dpi_ratio': mpl.ratio});
            }
            fig.send_message("refresh", {});
        }

    this.imageObj.onload = function() {
            if (fig.image_mode == 'full') {
                // Full images could contain transparency (where diff images
                // almost always do), so we need to clear the canvas so that
                // there is no ghosting.
                fig.context.clearRect(0, 0, fig.canvas.width, fig.canvas.height);
            }
            fig.context.drawImage(fig.imageObj, 0, 0);
        };

    this.imageObj.onunload = function() {
        fig.ws.close();
    }

    this.ws.onmessage = this._make_on_message_function(this);

    this.ondownload = ondownload;
}

mpl.figure.prototype._init_header = function() {
    var titlebar = $(
        '<div class="ui-dialog-titlebar ui-widget-header ui-corner-all ' +
        'ui-helper-clearfix"/>');
    var titletext = $(
        '<div class="ui-dialog-title" style="width: 100%; ' +
        'text-align: center; padding: 3px;"/>');
    titlebar.append(titletext)
    this.root.append(titlebar);
    this.header = titletext[0];
}



mpl.figure.prototype._canvas_extra_style = function(canvas_div) {

}


mpl.figure.prototype._root_extra_style = function(canvas_div) {

}

mpl.figure.prototype._init_canvas = function() {
    var fig = this;

    var canvas_div = $('<div/>');

    canvas_div.attr('style', 'position: relative; clear: both; outline: 0');

    function canvas_keyboard_event(event) {
        return fig.key_event(event, event['data']);
    }

    canvas_div.keydown('key_press', canvas_keyboard_event);
    canvas_div.keyup('key_release', canvas_keyboard_event);
    this.canvas_div = canvas_div
    this._canvas_extra_style(canvas_div)
    this.root.append(canvas_div);

    var canvas = $('<canvas/>');
    canvas.addClass('mpl-canvas');
    canvas.attr('style', "left: 0; top: 0; z-index: 0; outline: 0")

    this.canvas = canvas[0];
    this.context = canvas[0].getContext("2d");

    var backingStore = this.context.backingStorePixelRatio ||
	this.context.webkitBackingStorePixelRatio ||
	this.context.mozBackingStorePixelRatio ||
	this.context.msBackingStorePixelRatio ||
	this.context.oBackingStorePixelRatio ||
	this.context.backingStorePixelRatio || 1;

    mpl.ratio = (window.devicePixelRatio || 1) / backingStore;

    var rubberband = $('<canvas/>');
    rubberband.attr('style', "position: absolute; left: 0; top: 0; z-index: 1;")

    var pass_mouse_events = true;

    canvas_div.resizable({
        start: function(event, ui) {
            pass_mouse_events = false;
        },
        resize: function(event, ui) {
            fig.request_resize(ui.size.width, ui.size.height);
        },
        stop: function(event, ui) {
            pass_mouse_events = true;
            fig.request_resize(ui.size.width, ui.size.height);
        },
    });

    function mouse_event_fn(event) {
        if (pass_mouse_events)
            return fig.mouse_event(event, event['data']);
    }

    rubberband.mousedown('button_press', mouse_event_fn);
    rubberband.mouseup('button_release', mouse_event_fn);
    // Throttle sequential mouse events to 1 every 20ms.
    rubberband.mousemove('motion_notify', mouse_event_fn);

    rubberband.mouseenter('figure_enter', mouse_event_fn);
    rubberband.mouseleave('figure_leave', mouse_event_fn);

    canvas_div.on("wheel", function (event) {
        event = event.originalEvent;
        event['data'] = 'scroll'
        if (event.deltaY < 0) {
            event.step = 1;
        } else {
            event.step = -1;
        }
        mouse_event_fn(event);
    });

    canvas_div.append(canvas);
    canvas_div.append(rubberband);

    this.rubberband = rubberband;
    this.rubberband_canvas = rubberband[0];
    this.rubberband_context = rubberband[0].getContext("2d");
    this.rubberband_context.strokeStyle = "#000000";

    this._resize_canvas = function(width, height) {
        // Keep the size of the canvas, canvas container, and rubber band
        // canvas in synch.
        canvas_div.css('width', width)
        canvas_div.css('height', height)

        canvas.attr('width', width * mpl.ratio);
        canvas.attr('height', height * mpl.ratio);
        canvas.attr('style', 'width: ' + width + 'px; height: ' + height + 'px;');

        rubberband.attr('width', width);
        rubberband.attr('height', height);
    }

    // Set the figure to an initial 600x600px, this will subsequently be updated
    // upon first draw.
    this._resize_canvas(600, 600);

    // Disable right mouse context menu.
    $(this.rubberband_canvas).bind("contextmenu",function(e){
        return false;
    });

    function set_focus () {
        canvas.focus();
        canvas_div.focus();
    }

    window.setTimeout(set_focus, 100);
}

mpl.figure.prototype._init_toolbar = function() {
    var fig = this;

    var nav_element = $('<div/>')
    nav_element.attr('style', 'width: 100%');
    this.root.append(nav_element);

    // Define a callback function for later on.
    function toolbar_event(event) {
        return fig.toolbar_button_onclick(event['data']);
    }
    function toolbar_mouse_event(event) {
        return fig.toolbar_button_onmouseover(event['data']);
    }

    for(var toolbar_ind in mpl.toolbar_items) {
        var name = mpl.toolbar_items[toolbar_ind][0];
        var tooltip = mpl.toolbar_items[toolbar_ind][1];
        var image = mpl.toolbar_items[toolbar_ind][2];
        var method_name = mpl.toolbar_items[toolbar_ind][3];

        if (!name) {
            // put a spacer in here.
            continue;
        }
        var button = $('<button/>');
        button.addClass('ui-button ui-widget ui-state-default ui-corner-all ' +
                        'ui-button-icon-only');
        button.attr('role', 'button');
        button.attr('aria-disabled', 'false');
        button.click(method_name, toolbar_event);
        button.mouseover(tooltip, toolbar_mouse_event);

        var icon_img = $('<span/>');
        icon_img.addClass('ui-button-icon-primary ui-icon');
        icon_img.addClass(image);
        icon_img.addClass('ui-corner-all');

        var tooltip_span = $('<span/>');
        tooltip_span.addClass('ui-button-text');
        tooltip_span.html(tooltip);

        button.append(icon_img);
        button.append(tooltip_span);

        nav_element.append(button);
    }

    var fmt_picker_span = $('<span/>');

    var fmt_picker = $('<select/>');
    fmt_picker.addClass('mpl-toolbar-option ui-widget ui-widget-content');
    fmt_picker_span.append(fmt_picker);
    nav_element.append(fmt_picker_span);
    this.format_dropdown = fmt_picker[0];

    for (var ind in mpl.extensions) {
        var fmt = mpl.extensions[ind];
        var option = $(
            '<option/>', {selected: fmt === mpl.default_extension}).html(fmt);
        fmt_picker.append(option)
    }

    // Add hover states to the ui-buttons
    $( ".ui-button" ).hover(
        function() { $(this).addClass("ui-state-hover");},
        function() { $(this).removeClass("ui-state-hover");}
    );

    var status_bar = $('<span class="mpl-message"/>');
    nav_element.append(status_bar);
    this.message = status_bar[0];
}

mpl.figure.prototype.request_resize = function(x_pixels, y_pixels) {
    // Request matplotlib to resize the figure. Matplotlib will then trigger a resize in the client,
    // which will in turn request a refresh of the image.
    this.send_message('resize', {'width': x_pixels, 'height': y_pixels});
}

mpl.figure.prototype.send_message = function(type, properties) {
    properties['type'] = type;
    properties['figure_id'] = this.id;
    this.ws.send(JSON.stringify(properties));
}

mpl.figure.prototype.send_draw_message = function() {
    if (!this.waiting) {
        this.waiting = true;
        this.ws.send(JSON.stringify({type: "draw", figure_id: this.id}));
    }
}


mpl.figure.prototype.handle_save = function(fig, msg) {
    var format_dropdown = fig.format_dropdown;
    var format = format_dropdown.options[format_dropdown.selectedIndex].value;
    fig.ondownload(fig, format);
}


mpl.figure.prototype.handle_resize = function(fig, msg) {
    var size = msg['size'];
    if (size[0] != fig.canvas.width || size[1] != fig.canvas.height) {
        fig._resize_canvas(size[0], size[1]);
        fig.send_message("refresh", {});
    };
}

mpl.figure.prototype.handle_rubberband = function(fig, msg) {
    var x0 = msg['x0'] / mpl.ratio;
    var y0 = (fig.canvas.height - msg['y0']) / mpl.ratio;
    var x1 = msg['x1'] / mpl.ratio;
    var y1 = (fig.canvas.height - msg['y1']) / mpl.ratio;
    x0 = Math.floor(x0) + 0.5;
    y0 = Math.floor(y0) + 0.5;
    x1 = Math.floor(x1) + 0.5;
    y1 = Math.floor(y1) + 0.5;
    var min_x = Math.min(x0, x1);
    var min_y = Math.min(y0, y1);
    var width = Math.abs(x1 - x0);
    var height = Math.abs(y1 - y0);

    fig.rubberband_context.clearRect(
        0, 0, fig.canvas.width, fig.canvas.height);

    fig.rubberband_context.strokeRect(min_x, min_y, width, height);
}

mpl.figure.prototype.handle_figure_label = function(fig, msg) {
    // Updates the figure title.
    fig.header.textContent = msg['label'];
}

mpl.figure.prototype.handle_cursor = function(fig, msg) {
    var cursor = msg['cursor'];
    switch(cursor)
    {
    case 0:
        cursor = 'pointer';
        break;
    case 1:
        cursor = 'default';
        break;
    case 2:
        cursor = 'crosshair';
        break;
    case 3:
        cursor = 'move';
        break;
    }
    fig.rubberband_canvas.style.cursor = cursor;
}

mpl.figure.prototype.handle_message = function(fig, msg) {
    fig.message.textContent = msg['message'];
}

mpl.figure.prototype.handle_draw = function(fig, msg) {
    // Request the server to send over a new figure.
    fig.send_draw_message();
}

mpl.figure.prototype.handle_image_mode = function(fig, msg) {
    fig.image_mode = msg['mode'];
}

mpl.figure.prototype.updated_canvas_event = function() {
    // Called whenever the canvas gets updated.
    this.send_message("ack", {});
}

// A function to construct a web socket function for onmessage handling.
// Called in the figure constructor.
mpl.figure.prototype._make_on_message_function = function(fig) {
    return function socket_on_message(evt) {
        if (evt.data instanceof Blob) {
            /* FIXME: We get "Resource interpreted as Image but
             * transferred with MIME type text/plain:" errors on
             * Chrome.  But how to set the MIME type?  It doesn't seem
             * to be part of the websocket stream */
            evt.data.type = "image/png";

            /* Free the memory for the previous frames */
            if (fig.imageObj.src) {
                (window.URL || window.webkitURL).revokeObjectURL(
                    fig.imageObj.src);
            }

            fig.imageObj.src = (window.URL || window.webkitURL).createObjectURL(
                evt.data);
            fig.updated_canvas_event();
            fig.waiting = false;
            return;
        }
        else if (typeof evt.data === 'string' && evt.data.slice(0, 21) == "data:image/png;base64") {
            fig.imageObj.src = evt.data;
            fig.updated_canvas_event();
            fig.waiting = false;
            return;
        }

        var msg = JSON.parse(evt.data);
        var msg_type = msg['type'];

        // Call the  "handle_{type}" callback, which takes
        // the figure and JSON message as its only arguments.
        try {
            var callback = fig["handle_" + msg_type];
        } catch (e) {
            console.log("No handler for the '" + msg_type + "' message type: ", msg);
            return;
        }

        if (callback) {
            try {
                // console.log("Handling '" + msg_type + "' message: ", msg);
                callback(fig, msg);
            } catch (e) {
                console.log("Exception inside the 'handler_" + msg_type + "' callback:", e, e.stack, msg);
            }
        }
    };
}

// from http://stackoverflow.com/questions/1114465/getting-mouse-location-in-canvas
mpl.findpos = function(e) {
    //this section is from http://www.quirksmode.org/js/events_properties.html
    var targ;
    if (!e)
        e = window.event;
    if (e.target)
        targ = e.target;
    else if (e.srcElement)
        targ = e.srcElement;
    if (targ.nodeType == 3) // defeat Safari bug
        targ = targ.parentNode;

    // jQuery normalizes the pageX and pageY
    // pageX,Y are the mouse positions relative to the document
    // offset() returns the position of the element relative to the document
    var x = e.pageX - $(targ).offset().left;
    var y = e.pageY - $(targ).offset().top;

    return {"x": x, "y": y};
};

/*
 * return a copy of an object with only non-object keys
 * we need this to avoid circular references
 * http://stackoverflow.com/a/24161582/3208463
 */
function simpleKeys (original) {
  return Object.keys(original).reduce(function (obj, key) {
    if (typeof original[key] !== 'object')
        obj[key] = original[key]
    return obj;
  }, {});
}

mpl.figure.prototype.mouse_event = function(event, name) {
    var canvas_pos = mpl.findpos(event)

    if (name === 'button_press')
    {
        this.canvas.focus();
        this.canvas_div.focus();
    }

    var x = canvas_pos.x * mpl.ratio;
    var y = canvas_pos.y * mpl.ratio;

    this.send_message(name, {x: x, y: y, button: event.button,
                             step: event.step,
                             guiEvent: simpleKeys(event)});

    /* This prevents the web browser from automatically changing to
     * the text insertion cursor when the button is pressed.  We want
     * to control all of the cursor setting manually through the
     * 'cursor' event from matplotlib */
    event.preventDefault();
    return false;
}

mpl.figure.prototype._key_event_extra = function(event, name) {
    // Handle any extra behaviour associated with a key event
}

mpl.figure.prototype.key_event = function(event, name) {

    // Prevent repeat events
    if (name == 'key_press')
    {
        if (event.which === this._key)
            return;
        else
            this._key = event.which;
    }
    if (name == 'key_release')
        this._key = null;

    var value = '';
    if (event.ctrlKey && event.which != 17)
        value += "ctrl+";
    if (event.altKey && event.which != 18)
        value += "alt+";
    if (event.shiftKey && event.which != 16)
        value += "shift+";

    value += 'k';
    value += event.which.toString();

    this._key_event_extra(event, name);

    this.send_message(name, {key: value,
                             guiEvent: simpleKeys(event)});
    return false;
}

mpl.figure.prototype.toolbar_button_onclick = function(name) {
    if (name == 'download') {
        this.handle_save(this, null);
    } else {
        this.send_message("toolbar_button", {name: name});
    }
};

mpl.figure.prototype.toolbar_button_onmouseover = function(tooltip) {
    this.message.textContent = tooltip;
};
mpl.toolbar_items = [["Home", "Reset original view", "fa fa-home icon-home", "home"], ["Back", "Back to previous view", "fa fa-arrow-left icon-arrow-left", "back"], ["Forward", "Forward to next view", "fa fa-arrow-right icon-arrow-right", "forward"], ["", "", "", ""], ["Pan", "Pan axes with left mouse, zoom with right", "fa fa-arrows icon-move", "pan"], ["Zoom", "Zoom to rectangle", "fa fa-square-o icon-check-empty", "zoom"], ["", "", "", ""], ["Download", "Download plot", "fa fa-floppy-o icon-save", "download"]];

mpl.extensions = ["eps", "jpeg", "pdf", "png", "ps", "raw", "svg", "tif"];

mpl.default_extension = "png";var comm_websocket_adapter = function(comm) {
    // Create a "websocket"-like object which calls the given IPython comm
    // object with the appropriate methods. Currently this is a non binary
    // socket, so there is still some room for performance tuning.
    var ws = {};

    ws.close = function() {
        comm.close()
    };
    ws.send = function(m) {
        //console.log('sending', m);
        comm.send(m);
    };
    // Register the callback with on_msg.
    comm.on_msg(function(msg) {
        //console.log('receiving', msg['content']['data'], msg);
        // Pass the mpl event to the overridden (by mpl) onmessage function.
        ws.onmessage(msg['content']['data'])
    });
    return ws;
}

mpl.mpl_figure_comm = function(comm, msg) {
    // This is the function which gets called when the mpl process
    // starts-up an IPython Comm through the "matplotlib" channel.

    var id = msg.content.data.id;
    // Get hold of the div created by the display call when the Comm
    // socket was opened in Python.
    var element = $("#" + id);
    var ws_proxy = comm_websocket_adapter(comm)

    function ondownload(figure, format) {
        window.open(figure.imageObj.src);
    }

    var fig = new mpl.figure(id, ws_proxy,
                           ondownload,
                           element.get(0));

    // Call onopen now - mpl needs it, as it is assuming we've passed it a real
    // web socket which is closed, not our websocket->open comm proxy.
    ws_proxy.onopen();

    fig.parent_element = element.get(0);
    fig.cell_info = mpl.find_output_cell("<div id='" + id + "'></div>");
    if (!fig.cell_info) {
        console.error("Failed to find cell for figure", id, fig);
        return;
    }

    var output_index = fig.cell_info[2]
    var cell = fig.cell_info[0];

};

mpl.figure.prototype.handle_close = function(fig, msg) {
    var width = fig.canvas.width/mpl.ratio
    fig.root.unbind('remove')

    // Update the output cell to use the data from the current canvas.
    fig.push_to_output();
    var dataURL = fig.canvas.toDataURL();
    // Re-enable the keyboard manager in IPython - without this line, in FF,
    // the notebook keyboard shortcuts fail.
    IPython.keyboard_manager.enable()
    $(fig.parent_element).html('<img src="' + dataURL + '" width="' + width + '">');
    fig.close_ws(fig, msg);
}

mpl.figure.prototype.close_ws = function(fig, msg){
    fig.send_message('closing', msg);
    // fig.ws.close()
}

mpl.figure.prototype.push_to_output = function(remove_interactive) {
    // Turn the data on the canvas into data in the output cell.
    var width = this.canvas.width/mpl.ratio
    var dataURL = this.canvas.toDataURL();
    this.cell_info[1]['text/html'] = '<img src="' + dataURL + '" width="' + width + '">';
}

mpl.figure.prototype.updated_canvas_event = function() {
    // Tell IPython that the notebook contents must change.
    IPython.notebook.set_dirty(true);
    this.send_message("ack", {});
    var fig = this;
    // Wait a second, then push the new image to the DOM so
    // that it is saved nicely (might be nice to debounce this).
    setTimeout(function () { fig.push_to_output() }, 1000);
}

mpl.figure.prototype._init_toolbar = function() {
    var fig = this;

    var nav_element = $('<div/>')
    nav_element.attr('style', 'width: 100%');
    this.root.append(nav_element);

    // Define a callback function for later on.
    function toolbar_event(event) {
        return fig.toolbar_button_onclick(event['data']);
    }
    function toolbar_mouse_event(event) {
        return fig.toolbar_button_onmouseover(event['data']);
    }

    for(var toolbar_ind in mpl.toolbar_items){
        var name = mpl.toolbar_items[toolbar_ind][0];
        var tooltip = mpl.toolbar_items[toolbar_ind][1];
        var image = mpl.toolbar_items[toolbar_ind][2];
        var method_name = mpl.toolbar_items[toolbar_ind][3];

        if (!name) { continue; };

        var button = $('<button class="btn btn-default" href="#" title="' + name + '"><i class="fa ' + image + ' fa-lg"></i></button>');
        button.click(method_name, toolbar_event);
        button.mouseover(tooltip, toolbar_mouse_event);
        nav_element.append(button);
    }

    // Add the status bar.
    var status_bar = $('<span class="mpl-message" style="text-align:right; float: right;"/>');
    nav_element.append(status_bar);
    this.message = status_bar[0];

    // Add the close button to the window.
    var buttongrp = $('<div class="btn-group inline pull-right"></div>');
    var button = $('<button class="btn btn-mini btn-primary" href="#" title="Stop Interaction"><i class="fa fa-power-off icon-remove icon-large"></i></button>');
    button.click(function (evt) { fig.handle_close(fig, {}); } );
    button.mouseover('Stop Interaction', toolbar_mouse_event);
    buttongrp.append(button);
    var titlebar = this.root.find($('.ui-dialog-titlebar'));
    titlebar.prepend(buttongrp);
}

mpl.figure.prototype._root_extra_style = function(el){
    var fig = this
    el.on("remove", function(){
	fig.close_ws(fig, {});
    });
}

mpl.figure.prototype._canvas_extra_style = function(el){
    // this is important to make the div 'focusable
    el.attr('tabindex', 0)
    // reach out to IPython and tell the keyboard manager to turn it's self
    // off when our div gets focus

    // location in version 3
    if (IPython.notebook.keyboard_manager) {
        IPython.notebook.keyboard_manager.register_events(el);
    }
    else {
        // location in version 2
        IPython.keyboard_manager.register_events(el);
    }

}

mpl.figure.prototype._key_event_extra = function(event, name) {
    var manager = IPython.notebook.keyboard_manager;
    if (!manager)
        manager = IPython.keyboard_manager;

    // Check for shift+enter
    if (event.shiftKey && event.which == 13) {
        this.canvas_div.blur();
        event.shiftKey = false;
        // Send a "J" for go to next cell
        event.which = 74;
        event.keyCode = 74;
        manager.command_mode();
        manager.handle_keydown(event);
    }
}

mpl.figure.prototype.handle_save = function(fig, msg) {
    fig.ondownload(fig, null);
}


mpl.find_output_cell = function(html_output) {
    // Return the cell and output element which can be found *uniquely* in the notebook.
    // Note - this is a bit hacky, but it is done because the "notebook_saving.Notebook"
    // IPython event is triggered only after the cells have been serialised, which for
    // our purposes (turning an active figure into a static one), is too late.
    var cells = IPython.notebook.get_cells();
    var ncells = cells.length;
    for (var i=0; i<ncells; i++) {
        var cell = cells[i];
        if (cell.cell_type === 'code'){
            for (var j=0; j<cell.output_area.outputs.length; j++) {
                var data = cell.output_area.outputs[j];
                if (data.data) {
                    // IPython >= 3 moved mimebundle to data attribute of output
                    data = data.data;
                }
                if (data['text/html'] == html_output) {
                    return [cell, data, j];
                }
            }
        }
    }
}

// Register the function which deals with the matplotlib target/channel.
// The kernel may be null if the page has been refreshed.
if (IPython.notebook.kernel != null) {
    IPython.notebook.kernel.comm_manager.register_target('matplotlib', mpl.mpl_figure_comm);
}

</script>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>



<div class="output_html rendered_html output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABkAAAASwCAYAAACjAYaXAAAgAElEQVR4XuzdC9htU70/8OESctkukTpycunQSXHoQkQXKYSSSimSWzcRQqJCpRRFCR3Sg25KOpVQdHTQRYqTTp3kmq7I3sjtz373/j9jHe9qe7d3j7X2mnPMOeb6rOc5z7+93zHHGPPzG8Z+1/z+55yLzJ07d27wIUCAAAECBAgQIECAAAECBAgQIECAAAECBAh0SGARAUiHqulUCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgZ6AAMRCIECAAAECBAgQIECAAAECBAgQIECAAAECBDonIADpXEmdEAECBAgQIECAAAECBAgQIECAAAECBAgQICAAsQYIECBAgAABAgQIECBAgAABAgQIECBAgACBzgkIQDpXUidEgAABAgQIECBAgAABAgQIECBAgAABAgQICECsAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBzAgKQzpXUCREgQIAAAQIECBAgQIAAAQIECBAgQIAAAQICEGuAAAECBAgQIECAAAECBAgQIECAAAECBAgQ6JyAAKRzJXVCBAgQIECAAAECBAgQIECAAAECBAgQIECAgADEGiBAgAABAgQIECBAgAABAgQIECBAgAABAgQ6JyAA6VxJnRABAgQIECBAgAABAgQIECBAgAABAgQIECAgALEGCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgc4JCEA6V1InRIAAAQIECBAgQIAAAQIECBAgQIAAAQIECAhArAECBAgQIECAAAECBAgQIECAAAECBAgQIECgcwICkM6V1AkRIECAAAECBAgQIECAAAECBAgQIECAAAECAhBrgAABAgQIECBAgAABAgQIECBAgAABAgQIEOicgACkcyV1QgQIECBAgAABAgQIECBAgAABAgQIECBAgIAAxBogQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOicgAOlcSZ0QAQIECBAgQIAAAQIECBAgQIAAAQIECBAgIACxBggQIECAAAECBAgQIECAAAECBAgQIECAAIHOCQhAOldSJ0SAAAECBAgQIECAAAECBAgQIECAAAECBAgIQKwBAgQIECBAgAABAgQIECBAgAABAgQIECBAoHMCApDOldQJESBAgAABAgQIECBAgAABAgQIECBAgAABAgIQa4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBDonIAApHMldUIECBAgQIAAAQIECBAgQIAAAQIECBAgQICAAMQaIECAAAECBAgQIECAAAECBAgQIECAAAECBDonIADpXEmdEAECBAgQIECAAAECBAgQIECAAAECBAgQICAAsQYIECBAgAABAgQIECBAgAABAgQIECBAgACBzgkIQDpXUidEgAABAgQIECBAgAABAgQIECBAgAABAgQICECsAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBzAgKQzpXUCREgQIAAAQIECBAgQIAAAQIECBAgQIAAAQICEGuAAAECBAgQIECAAAECBAgQIECAAAECBAgQ6JyAAKRzJXVCBAgQIECAAAECBAgQIECAAAECBAgQIECAgADEGiBAgAABAgQIECBAgAABAgQIECBAgAABAgQ6JyAA6VxJnRABAgQIECBAgAABAgQIECBAgAABAgQIECAgALEGCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgc4JCEA6V1InRIAAAQIECBAgQIAAAQIECBAgQIAAAQIECAhArAECBAgQIECAAAECBAgQIECAAAECBAgQIECgcwICkM6V1AkRIECAAAECBAgQIECAAAECBAgQIECAAAECAhBrgAABAgQIECBAgAABAgQIECBAgAABAgQIEOicgACkcyV1QgQIECBAgAABAgQIECBAgAABAgQIECBAgIAAxBogQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOicgAOlcSZ0QAQIECBAgQIAAAQIECBAgQIAAAQIECBAgIACxBggQIECAAAECBAgQIECAAAECBAgQIECAAIHOCQhAOldSJ0SAAAECBAgQIECAAAECBAgQIECAAAECBAgIQKwBAgQIECBAgAABAgQIECBAgAABAgQIECBAoHMCApDOldQJESBAgAABAgQIECBAgAABAgQIECBAgAABAgIQa4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBDonIAApHMldUIECBAgQIAAAQIECBAgQIAAAQIECBAgQICAAMQaIECAAAECBAgQIECAAAECBAgQIECAAAECBDonIADpXEmdEAECBAgQIECAAAECBAgQIECAAAECBAgQICAAsQYIECBAgAABAgQIECBAgAABAgQIECBAgACBzgkIQDpXUidEgAABAgQIECBAgAABAgQIECBAgAABAgQICECsAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBzAgKQzpXUCREgQIAAAQIECBAgQIAAAQIECBAgQIAAAQICEGuAAAECBAgQIECAAAECBAgQIECAAAECBAgQ6JyAAKRzJXVCBAgQIECAAAECBAgQIECAAAECBAgQIECAgADEGiBAgAABAgQIECBAgAABAgQIECBAgAABAgQ6JyAA6VxJnRABAgQIECBAgAABAgQIECBAgAABAgQIECAgALEGCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgc4JCEA6V1InRIAAAQIECBAgQIAAAQIECBAgQIAAAQIECAhArAECBAgQIECAAAECBAgQIECAAAECBAgQIECgcwICkM6V1AkRIECAAAECBAgQIECAAAECBAgQIECAAAECAhBrgAABAgQIECBAgAABAgQIECBAgAABAgQIEOicgACkcyV1QgQIECBAgAABAgQIECBAgAABAgQIECBAgIAAxBogQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOicgAOlcSZ0QAQIECBAgQIAAAQIECBAgQIAAAQIECBAgIACxBggQIECAAAECBAgQIECAAAECBAgQIECAAIHOCQhAOldSJ0SAAAECBAgQIECAAAECBAgQIECAAAECBAgIQKwBAgQIECBAgAABAgQIECBAgAABAgQIECBAoHMCApDOldQJESBAgAABAgQIECBAgAABAgQIECBAgAABAgIQa4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBDonIAApHMldUIECBAgQIAAAQIECBAgQIAAAQIECBAgQICAAMQaIECAAAECBAgQIECAAAECBAgQIECAAAECBDonIADpXEmdEAECBAgQIECAAAECBAgQIECAAAECBAgQICAAsQYIECBAgAABAgQIECBAgAABAgQIECBAgACBzgkIQDpXUidEgAABAgQIECBAgAABAgQIECBAgAABAgQICECsAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBzAgKQzpXUCREgQIAAAQIECBAgQIAAAQIECBAgQIAAAQICEGuAAAECBAgQIECAAAECBAgQIECAAAECBAgQ6JyAAKRzJXVCBAgQIECAAAECBAgQIECAAAECBAgQIECAgADEGiBAgAABAgQIECBAgAABAgQIECBAgAABAgQ6JyAA6VxJnRABAgQIECBAgAABAgQIECBAgAABAgQIECAgALEGCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgc4JCEA6V1InRIAAAQIECBAgQIAAAQIECBAgQIAAAQIECAhArAECBAgQIECAAAECBAgQIECAAAECBAgQIECgcwICkM6V1AkRIECAAAECBAgQIECAAAECBAgQIECAAAECAhBrgAABAgQIECBAgAABAgQIECBAgAABAgQIEOicgACkcyV1QgQIECBAgAABAgQIECBAgAABAgQIECBAgIAAxBogQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOicgAOlcSZ0QAQIECBAgQIAAAQIECBAgQIAAAQIECBAgIACxBggQIECAAAECBAgQIECAAAECBAgQIECAAIHOCQhAOldSJ0SAAAECBAgQIECAAAECBAgQIECAAAECBAgIQKwBAgQIECBAgAABAgQIECBAgAABAgQIECBAoHMCApDOldQJESBAgAABAgQIECBAgAABAgQIECBAgAABAgIQa4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBDonIAApHMldUIECBAgQIAAAQIECBAgQIAAAQIECBAgQICAAMQaIECAAAECBAgQIECAAAECBAgQIECAAAECBDonIADpXEmdEAECBAgQIECAAAECBAgQIECAAAECBAgQICAAsQYIECBAgAABAgQIECBAgAABAgQIECBAgACBzgkIQDpXUidEgAABAgQIECBAgAABAgQIECBAgAABAgQICECsAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBzAgKQzpXUCREgQIAAAQIECBAgQIAAAQIECBAgQIAAAQICEGuAAAECBAgQIECAAAECBAgQIECAAAECBAgQ6JyAAKRzJXVCBAgQIECAAAECBAgQIECAAAECBAgQIECAgADEGiBAgAABAgQIECBAgAABAgQIECBAgAABAgQ6JyAA6VxJnRABAgQIECBAgAABAgQIECBAgAABAgQIECAgALEGCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgc4JCEA6V1InRIAAAQIECBAgQIAAAQIECBAgQIAAAQIECAhArAECBAgQIECAAAECBAgQIECAAAECBAgQIECgcwICkM6V1AkRIECAAAECBAgQIECAAAECBAgQIECAAAECAhBrgAABAgQIECBAgAABAgQIECBAgAABAgQIEOicgACkcyV1QgQIECBAgAABAgQIECBAgAABAgQIECBAgIAAxBogQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOicgAOlcSZ0QAQIECBAgQIAAAQIECBAgQIAAAQIECBAgIACxBggQIECAAAECBAgQIECAAAECBAgQIECAAIHOCQhAOldSJ0SAAAECBAgQIECAAAECBAgQIECAAAECBAgIQKwBAgQIECBAgAABAgQIECBAgAABAgQIECBAoHMCApDOldQJESBAgAABAgQIECBAgAABAgQIECBAgAABAgIQa4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBDonIAApHMldUIECBAgQIAAAQIECBAgQIAAAQIECBAgQICAAMQaIECAAAECBAgQIECAAAECBAgQIECAAAECBDonIADpXEmdEAECBAgQIECAAAECBAgQIECAAAECBAgQICAAsQYIECBAgAABAgQIECBAgAABAgQIECBAgACBzgkIQDpXUidEgAABAgQIECBAgAABAgQIECBAgAABAgQICECsAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBzAgKQzpXUCREgQIAAAQIECBAgQIAAAQIECBAgQIAAAQICEGuAAAECBAgQIECAAAECBAgQIECAAAECBAgQ6JyAAKRzJXVCBAgQIECAAAECBAgQIECAAAECBAgQIECAgADEGiBAgAABAgQIECBAgAABAgQIECBAgAABAgQ6JyAA6VxJnRABAgQIECBAgAABAgQIECBAgAABAgQIECAgALEGCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgc4JCEA6V1InRIAAAQIECBAgQIAAAQIECBAgQIAAAQIECAhArAECBAgQIECAAAECBAgQIECAAAECBAgQIECgcwICkM6V1AkRIECAAAECBAgQIECAAAECBAgQIECAAAECAhBrgAABAgQIECBAgAABAgQIECBAgAABAgQIEOicgACkcyV1QgQIECBAgAABAgQIECBAgAABAgQIECBAgIAAxBogQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOicgAOlcSZ0QAQIECBAgQIAAAQIECBAgQIAAAQIECBAgIACxBggQIECAAAECBAgQIECAAAEC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FfBloa2VMS8C5QjYR8qplZkSaKuAfaStlTEvAmUI2EPy1EkAksfZKGkBAUjaqNIWwwQgc+fODc985jP7j52Kocruu+8+0Hxe9rKXhd///ve9tlPv1thtt93ClVde2ftZfBzXySefPFCfMeCIQUf8TL1bI96Z8pnPfKb3s+WWWy7EO0IG+fxv7GoAACAASURBVMT3kxx88MH9pvFF6FPfLTJIP3W3EYDULax/AgRKEfBloZRKmSeB9grYR9pbGzMjUIqAfaSUSpkngXYK2EPy1EUAksfZKGkBAUjaqNIWwwQg8SXh8S6SyU98P0Z8T8Ygn9ju17/+da/pdttt13sh++Rnhx12CNddd13vj/E9HvF9HoN85n25+iqrrNJ7Efrk58Mf/nA4++yze3+M7xuJ7x0Z5DPvy9Vj+4suuiisueaagxyatc3ddz8Q5syZm3XMugaL/wDNmLFUv/t77nkwTEzMqWs4/RIg0DEBe0jHCup0CDQgYB9pAN2QBDomYB/pWEGdDoHMAvaQPOCLLrpIWH759NNh8szGKOMsIADJXP1hApDbb789bL755v0ZfupTn+q/SyQ17XlfLj713SEvf/nLwy233NLrIrabfDl7qs84/qmnntprNvXdIR/4wAfCOeec0/vZWmutFS688MJUd72f/+hHPwp77LFHv+2g7w4ZqHONCBAgQIAAAQIECBAgQIAAAQIECBAgQGBsBQQgmUs/TADy5z//Obz4xS/uz/DEE08MW2+99UAzftOb3hSuuuqqXtvYx2RwEf8cH3sV5xE/b3zjG0MMLwb5xBenxxeox88yyywTrr766v5h8fFc5513Xu/P//Iv/xLOP//8QbrsveA9vuh98hP7WG+99QY6ViMCBAgQIECAAAECBAgQIECAAAECBAgQIDCdgAAk89oYJgCJLz+PL0Gf/CzsHSDxjo8YXkx+5n0/yMLeAbLCCiv03yMS+533/SCj3AESX86+zjrrZK6K4QgQIECAAAECBAgQIECAAAECBAgQIECgawICkMwVHSYAmfoOkPgOjvjOjkE+874DZPvttw/HHXdc/7B53wES28V3iwzymfcdIKuuumq47LLL+odV9Q6Q73//++GpT33qINPJ2sY7QLJyG6xigfh80xI/3k3Tzqp5Xm4762JWBEoSsI+UVC1zJdBOAftIO+tiVgRKEbCH5KmUd4Dk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PwKQNlalmTkJQOpzF4DUZxt7LilUKGmu0VYAUu/a1Xv3BFx06F5NnRGB3AL2kdzixiPQLQF7SJ56CkDyOBslLSAASRu1okW8A2PHHXcMd911V28+8Y6O3Xffvfd/q666an+O9957b4jv0Tj55JP74ccKK6zQezn5aqut9qhz+cMf/tC7A+P+++/v/X28O+Soo44KL33pS/svWb/pppvCEUcc0Xvfx+Qn3lnyqle96jFdZs+eHeIdKtddd13v54973OPCfvvtF3bbbbew1FJL9f4unkN8HNc555zT72OnnXbqPwqrFeBTJiEAaWNVmpnTuAcgf7vo38P/u+33leAvuepTw8pb79PvSwBSCeu0nZQUKpQ01wguAKl37eq9ewIuOnSvps6IQG4B+0huceMR6JaAPSRPPQUgeZyNkhYQgKSNWtMihhB77713uO+++/pzikHImmuuGVZeeeUQw4/4+KnJx1TFRssss0w47bTTwrOf/ezHPI/4To/4fpF5j3niE58Y1lhjjV5Qcf3114e5c+f2j9155537LzqfDuaWW24Ju+66a7j99tv7TZZddtmwzjrr9B659dvf/jbEu0omP+utt1744he/2HsHSFs/ApC2Vib/vMY9APnTmYeH//fH31YCv+RTnh5We/NH+n0JQCphnbaTkkKFkuYawQUg9a5dvXdPwEWH7tXUGRHILWAfyS1uPALdErCH5KmnACSPs1HSAgKQtFGrWsRw4b3vfW+45pprkvP6t3/7txDv1ohhxoI+l112We8uj9tuu23aZosttlgvfIlhSXxcVepz6623hviIrWuvvXaBTV/ykpf03vux3HLLpbps9OcCkEb5WzW4AEQAMrkgS7tIX9J8S5qrAKRVW7TJFCLgokMhhTJNAi0WsI+0uDimRqAAAXtIniIJQPI4GyUtIABJG7WyxU9+8pNw0UUXhauvvrp3p0W8+yPeZRHv3thoo41CfOfH85///IHnHh+D9Y1vfCP84Ac/CDfeeGOIL15fYoklwlOe8pSwySabhHjnx9prrz1wf7FhvHPke9/7Xm+eMQi58847e8fHd4hsuOGGvUd6bbrppkP12VRjAUhT8u0bVwAiABGA1P/fpQCkfmMjEGhSwEWHJvWNTaAbAvaRbtTRWRBoSsAekkdeAJLH2ShpAQFI2kgLAkEAYhFMCghABCACkPr3AwFI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zDLEZJYJAVL+XltpBgKkHlszLycBhw7LmVdXhUBLAvpIS9rWQmD5COghbXJKgLThbJU4AQIkzkgEAgRIxRogQMrhOuwnQFKqiABJoTRfDAEyHzejxkvAocN4c+/KEVgUAX1kUSTNg8A4CeghbfJOgLThbJU4AQIkzkgEAgRIxRogQMrhEiAESEoVESAplOaLIUDm42bUeAk4dBhv7l05AosioI8siqR5EBgnAT2kTd4JkDacrRInQIDEGYlAgACpWAMESDlcAoQASakiAiSF0nwxBMh83IwaLwGHDuPNvStHYFEE9JFFkTQPAuMkoIe0yTsB0oazVeIECJA4IxEIECAVa4AAKYdLgBAgKVVEgKRQmi+GAJmPm1HjJeDQYby5d+UILIqAPrIokuZBYJwE9JA2eSdA2nC2SpwAARJn1NuIyy67LHzhC18IV1xxRfjRj34UfvrTn4a99947POxhDwv/5b/8l/Bf/+t/Dfe5z32S9n/XXXeFiy++OFxyySXh29/+dvjJT34S9thjj3DAAQeEo48+Opx44olhzZo1SXNtHfT1r389XHjhhdM97rzzzpM5jzjiiPDMZz4zHHvssdlzrsaAdetuD5s23b0aSy98zb79Q0+AlKeYACFAUqqIAEmhNF8MATIfN6PGS6Bvn0XGmwlXjsBwCegjw82dnSPQBwJ6SJssECBtOFslToAAiTPqXcR3v/vd8Pu///vhW9/61g739sAHPjCceeaZ4aijjtph3FVXXRVe+9rXhmuvvXbFuE5cvPCFLwyvec1rwr3vfe8ok1tvvTWceuqp4dJLL91hbCdA3v72t4f9998/OudqBhAg9egTIOVsCRACJKWKCJAUSvPFECDzcTNqvAQcOow3964cgUUR0EcWRdI8CIyTgB7SJu8ESBvOVokTIEDijHoV8Y//+I/hJS95SegEw5bXXnvtFQ477LCw6667hmuuuSb8v//3/6Z/62TF+973vsldHNt7dfLj5JNPDuvXr5/+eb/99pvM1/2um+/uu39558Nxxx0XzjrrrLDTTjutyOW2224LJ510Urj66qunMd3dJA996EMnc/3zP/9z2LBhw/Rvhx56aPjEJz4xuXulry8CpF5mCJBytgTILENMZpkQIOXvtZVmIEDqsTXzchJw6LCceXVVCLQkoI+0pG0tBJaPgB7SJqcESBvOVokTIEDijHoTceONN4ZnPetZU/nRSYU3vvGNk9/d6173muxz48aN4YILLgh/9Ed/NJUMndD4/Oc/HzpRsvXrjjvuCM94xjPC97///cmv99lnn/CWt7wlPPnJT54Kjn/9138Nf/AHfxC+9KUvTYe+/vWvDy996UtX5PK6170ufO5zn5v8fZdddgmvfvWrwwte8IKw++67T353++23hw984APh3HPPncqVxz/+8eH9739/b1hvuxECpF5qCJBytg77ZxliMsuEACl/r600AwFSj62Zl5OAQ4flzKurQqAlAX2kJW1rIbB8BPSQNjklQNpwtkqcAAESZ9SbiJe//OXhy1/+8mQ/++67b/jgBz8YHv7wh293f1/84hfDK1/5yunffvd3fze86EUvukfse9/73vDud7978rvuTpGPfexj4fDDD5+Zb/PmzaGTHlukxn3ve9+JEOmEybavb37zm+F5z3ve9Nenn376PX7eOv7jH/94ePOb3zz91Z//+Z+veKfKaieBAKmXAQKknK3D/lmGmMwyIUDK32srzUCA1GNr5uUk4NBhOfPqqhBoSUAfaUnbWggsHwE9pE1OCZA2nK0SJ0CAxBn1IqL7qqruTo8tr+5rqI4//vgd7u3Xf/3Xw5VXXjmJefSjHx0+8pGPTON/9rOfhSc84Qnh5ptvnvyukyOdJFnp1d218aQnPSmsW7duEtI9C+RlL3vZTHgnXTr50r0e8YhHhE9/+tM73GN3J8lXv/rVScwxxxwTPvShD/WC97abIEDqpYUAKWfrsH+WISazTAiQ8vfaSjMQIPXYmnk5CTh0WM68uioEWhLQR1rSthYCy0dAD2mTUwKkDWerxAkQIHFGvYh461vfGj784Q9P9tI91Pz888+P7qt7APnf//3fT+7UOOCAA+4hUC6//PLJs0S2vP7qr/4qPPjBD97hnN3XanV3aXSvNWvWhIsuuuge8Z0keexjHxs6udK9zjjjjPDc5z53h3P+zd/8TTjllFMmMd3XZX3ta1+b3N3StxcBUi8jBEg5W4f9swwxmWVCgJS/11aagQCpx9bMy0nAocNy5tVVIdCSgD7Skra1EFg+AnpIm5wSIG04WyVOgACJM+pFxK/92q+FG264YbKXd73rXeFpT3ta0b7OPPPM6d0WBx10UOhkSezVyYkXv/jF07BOXhx88MHTn7s5tr4rpPuarF/5lV/Z4bQ//elPJ3endM8u6V6dZDnxxBNjW2n+dwKkHnICpJytw/5ZhpjMMiFAyt9rK81AgNRja+blJODQYTnz6qoQaElAH2lJ21oILB8BPaRNTgmQNpytEidAgMQZrXrETTfdFLqHhG95dSKie7B5yat7KPnf/d3fTaboHnp+9tlnR6frvv7qV3/1V6dx234N15/92Z+FP/3TP538/X73u9/k7pOUVydzvvvd705CTzrppHs8FyRlfIsYAqQeZQKknK3D/lmGmMwyIUDK32srzUCA1GNr5uUk4NBhOfPqqhBoSUAfaUnbWggsHwE9pE1OCZA2nK0SJ0CAxBmtesRll10W1q5dO9nH3nvvHb7xjW9M/rsTEp/97Gcnz9y47rrrwq233jr5+qju2RsnnHDC5P923nnn7e6/EyqdWOle3V0db3jDG5Ku85GPfGTYsGHDJPa3f/u3p19f1f3cPSi920/3OuKII8KnPvWppDm7u0a23IFy9NFHT79mK2lwoyACpB5oAqScrcP+WYaYzDIhQMrfayvNQIDUY2vm5STg0GE58+qqEGhJQB9pSdtaCCwfAT2kTU4JkDacrRInQIDEGa16RPfsj+4ZIN3roQ996EQyfOYznwlvf/vbJ9JjpVcnQrq7NP7tv/239wjZvHlzOPzww6dfO/V7v/d74YUvfGHSdT7lKU8J119//SR227s1nv/850/lTPeVXe9973uT5nzTm94U/vIv/3IS+5CHPCRcfPHFSeNaBhEg9WgTIOVsHfbPMsRklgkBUv5eW2kGAqQeWzMvJwGHDsuZV1eFQEsC+khL2tZCYPkI6CFtckqAtOFslTgBAiTOaNUj/uRP/iSce+65k338x//4H0MnId7xjndM93XIIYeE7jke3UPIr7nmmulDyLuA7gHof/EXfzERJ1tenTR5zGMeM/35D//wD8Ozn/3spOvs4r797W9PYp/+9KeHP/7jP56Oe+Yznxmuvvrqyc/dczy653mkvLZ+uHr31V7dV3z17UWA1MsIAVLO1mH/LENMZpkQIOXvtZVmIEDqsTXzchJw6LCceXVVCLQkoI+0pG0tBJaPgB7SJqcESBvOVokTIEDijFY94owzzggf/ehHJ/vYc889w2233Ra6uzi6r6Pq7p7o7ubY8urkRnfnxf/+3/97+rsHPehB4dOf/nS4733vO/ndD3/4w3DsscdO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EtBDquKdTk6AtOFslTgBAiTOSAQCBEhGDRAgBEhqudQ82DY3uZJah+4AIUBSayUljgBJoRSCQ4c0TqIQQGBlAvqI6kAAgRICekgJvfSxBEg6K5F1CRAgdfmafUkIeAh6eiIJEAIktVpICpIipVZq1km3PgFCgKTUYWoMAZJGyqFDGidRCCBAgKgBBBCoQ8BnkTpct52VAGnD2SpxAgRInJEIBNwBklEDBAgBklouNQ+2zU2upNYhAUKApNZKSty2AuScC64M1924PmXoqsQceuBe4ZTnHDld21dgrUoaLIoAAnMQcHg5BzRDEEBgSkAPaVMMBEgbzlaJEyBA4oxEIECAZNQAAUKApJYLSUFSpNRKzTrp1idACJCUOkyNGdozSx5+2L7hzFceS4CkJlgcAgj0hoDDy96kwkYQGCQBPaRN2giQNpytEidAgMQZDSri85//fHjNa14z2fNjHvOY8OEPfzhp/3fddVe4+OKLwyWXXBK+/e1vh5/85Cdhjz32CAcccEA4+uijw4knnhjWrFmTNNfWQV//+tfDhRdeGK644orwox/9KOy8886TOY844ojwzGc+Mxx77C//R3f25A0H+AqsdNgECAGSWi01D7bNTa6k1iEBQoCk1kpKHAGSQskzQNIoiUIAgR0RcHipPhBAoISAHlJCL30sAZLOSmRdAgRIXb5NZ//hD38YnvGMZ0zkRY4Aueqqq8JrX/vacO211664305cvPCFL5zIlXvf+97R67r11lvDqaeeGi699NIdxnYC5O1vf3vYf//9o3OuZgABkk6fACFAUquFpCApUmqlZp106xMgBEhKHabGECBppBw6pHEShQACKxPQR1QHAgiUENBDSuiljyVA0lmJrEuAAKnLt+nsa9euDZdddtl0zZQ7QDr5cfLJJ4f163/5/dT77bdfOOywwya/u+aaa8Ldd989nfO4444LZ511Vthpp51WvLbbbrstnHTSSeHqq6+exnR3kzz0oQ+dzPXP//zPYcOGDdO/HXrooeETn/hE2HvvvZvyylmMAEmnRYAQIKnVUvNg29zkSmodEiAESGqtpMQRICmU3AGSRkkUAgjsiIDDS/WBAAIlBPSQEnrpYwmQdFYi6xIgQOrybTb7Jz/5yfD7v//791gvJkDuuOOOyR0j3//+9yfj9tlnn/CWt7wlPPnJT54Kjn/9138Nf/AHfxC+9KUvTed+/etfH1760peueG2ve93rwuc+97nJ33fZZZfw6le/OrzgBS8Iu+++++R3t99+e/jABz4Qzj333KlcefzjHx/e//73N+OVuxABkk6MANk+Kwfys1wwwSSls9Ssk259AoQASanD1BgCJI2UQ4c0TqIQQGBlAvqI6kAAgRICekgJvfSxBEg6K5F1CRAgdfk2mf2GG26YPE+jEwtbv2IC5L3vfW9497vfPRnSfa3Vxz72sXD44YfP7Hnz5s2hkx5bpMZ973vfiRDphMm2r29+85vhec973vTXp59++j1+3jr+4x//eHjzm988/dWf//mfT5430scXAZKeFQJk+6xqHuKae5Y5Jpikdi0ChABJrZWUOAIkhZI7QNIoiUIAgR0RcHipPhBAoISAHlJCL30sAZLOSmRdAgRIXb7VZ+++Uqq7u+Lv//7vJ2vttdde06+z2pEA+dnPfhae8IQnhJtvvnky7kUvelH43d/93RX328mVJz3pSWHdunWTmO5ZIC972ctm4l/5yleGL37xi5PfP+IRjwif/vSnd8igu5Pkq1/96iTmmGOOCR/60IeqM5tnAQIknRoBsn1WDuRnuWCCSUpnqVkn3foECAGSUoepMQRIGimHDmmcRCGAwMoE9BHVgQACJQT0kBJ66WMJkHRWIusSIEDq8q0+e3fXxB/90R9N1jnqqKPCAx/4wPCZz3xm8vOOBMjll18eXvKSl0z391d/9VfhwQ9+8A73263Trde91qxZEy666KJ7xHeS5LGPfWzo5Er3OuOMM8Jzn/vcHc75N3/zN+GUU06ZxHRfl/W1r30t7LvvvtW55S5AgKQTI0C2z6rmIa65Z5ljgklq1yJACJDUWkmJI0BSKLkDJI2SKAQQ2BEBh5fqAwEESgjoISX00scSIOmsRNYlQIDU5Vt19muvvTaceOKJ4c477wzdQ8Y/+9nPhve85z3hwgsvnKy7IwFy5plnTu+2OOigg8Kll14a3WsnJ1784hdP4zp5cfDBB09/7ubY+q6Q7muyfuVXfmWH8/70pz8Nj370o8PGjRsncZ1k6a6pby8CJD0jBMj2WTmQn+WCCSYpnaVmnXTrEyAESEodpsYQIGmkHDqkcRKFAAIrE9BHVAcCCJQQ0ENK6KWPJUDSWYmsS4AAqcu32uydMPjv//2/h3/6p3+arNE9qPzXf/3XJ19jlSJAuq/N+ru/+7vJ2O6h52effXZ0r93XX/3qr/7qNO6ss84Kxx9//PTnP/uzPwt/+qd/Ovn5fve73/RruWITP+1pTwvf/e53J2EnnXTSPZ4LEhvb6u8ESDppAmT7rGoe4pp7ljkmmKR2LQKEAEmtlZQ4AiSFkjtA0iiJQgCBHRFweKk+EECghIAeUkIvfSwBks5KZF0CBEhdvtVm74RFd7dH93rc4x4XPvjBD07+O1WAPP7xjw833XTTZEx3V8cb3vCGpL0+8pGPDBs2bJjE/vZv//b066u6n7sHpXd3oXSvI444InzqU59KmrO7a2TLHSjdQ9C3fM1W0uBGQQRIOmgCZPusHMjPcsEEk5TOUrNOuvUJEAIkpQ5TYwiQNFIOHdI4iUIAgZUJ6COqAwEESgjoISX00scSIOmsRNYlQIDU5Vtl9u6uj+7uj+4ukD333DN87nOfmzz7o3ulCJDNmzeHww8/fPq1U7/3e78XXvjCFybt9SlPeUq4/vrrJ7Hb3q3x/Oc/P3zjG9+Y/O3Xfu3Xwnvf+96kOd/0pjeFv/zLv5zEPuQhDwkXX3xx0riWQQRIOm0CZPusah7imnuWOSaYpHYtAoQASa2VlDgCJIWSO0DSKIlCAIEdEXB4qT4QQKCEgB5SQi99LAGSzkpkXQIESF2+C5/9rrvumjwjY8tXRv3hH/5hePaznz1dJ0WA3HrrrZPng2x5bTvHjjbdrfXtb397EvL0pz89/PEf//E0/JnPfGa4+uqrJz93e9zycPYYhK0frr7ffvtNHoTetxcBkp4RAmT7rBzIz3LBBJOUzlKzTrr1CRACJKUOU2MIkDRSDh3SOIlCAIGVCegjqgMBBEoI6CEl9NLHEiDprETWJUCA1OW78Nm3fnj5E57whPC+973vHmukCJAf/vCH4dhjj52O+5M/+ZNwwgknJO31uc99brjiiismsds+O+SpT31quO666yZ/6+LOOOOMpDm79c8999xJbM6zQ5ImX1DQrbf+NNx99+YFzba603T/AO211+7TTaxff0fYtOnuhW1q2/l/cP5p4c4brlrY/DUPQ809myZMMEl58w61TrprI0AIkJQaT40ZugBZ9GeClbjV/iySmi9xCCAwXAL6yHBzZ+cI9IGAHtImCzvvvFO43/3+TZvFrILADggQIAMqj29+85vh5JNPDnffffdEFHRffbX//vvf4wpSBMi//Mu/hCc+8YnTce9+97vDcccdl0TiN37jN8I//MM/TGK7ObaIi+7n7muvbrjhhsnfnve854XTTz89ac7uwendA9S71x577BG+9a1vJY0TNAwCBMjP8zTUA2L7nn2fYbI8TLorIUAIkEX+azp0AbJIFuZCAAEEEEAAAQQQQAABBPpAgADpQxYS9nD77beHZz3rWeH//t//O4n+X//rf4XuK6e2faUIkO7h591D0Le85r0DpLvjo5MXW15bPx9k3jtA9t577+lzRBKwCBkAAQLk50lyaD5brJhgktLCatZJtz4BQoCk1GFqDAGSSkocAggggAACCCCAAAIIINCGAAHShnPxKt3dFJ/4xCcm8zzpSU+a3jGx7cQpAmTbZ4B0z+DontmR8tr6GSDPeMYzwjvf+c7psK2fAdLFdc8WSXlt/QyQAw44IHz1q19NGSZmIAQIkJ8nquYhrrln3wyYYJLaIgkQAiS1VlLiCJAUSmIQQAABBBBAAAEEEEAAgXYECJB2rOdeqRMCL33pSyfj99lnn8lXXz3gAQ/Y7nwpAmTz5s3hEY94RNi0adNkjtNOOy08//nPT9pf99yP73//+5PY7uu43vSmN03HdXN84xvfmPy87fNBdjR5t/6nPvWpSciaNWvCRRddlLSXlkGeAZJO2zNAts/KgfwsF0wwSeksNeukW58AIUBS6jA1ZugCxDNAUjMtDgEEVpuA7+9f7QxYH4FhE9BD2uTPM0DacLZKnAABEme0qhHd3RpPf/rTQ/fg8u4V+7qqFAHSzdN9BVb3VVjd62Uve1l4zWtek3Sdj3zkI8OGDRsmsa973evC2rVrp+Ne//rXh89+9rOTn7u4j3/840lz/tZv/Vb4yle+Mol93OMeFz74wQ8mjWsZtG7d7Qt9UHjLvW+71q677hL22ec+01/fcsuGsHHjz2XYIl7bzu8OkJ9TrXmIa+7ZysUEk9R+RoAQIKm1khI3dAGy6M8EKzGr/VkkJVdiEEBg2AT0kWHnz+4RWG0CekibDHSiad9992izmFUQ2AEBAqTn5fG+970vvOtd75rs8l73uld47GMfu8MdX3PNNVNZ0j0o/YgjjpjG/+Zv/mY45phjJj9vfbfG8ccfH84666woiR//+Mfh6KOPnsZ1Dy7vvo5ry+vss88O73nPeyY/3v/+9w9f//rXo3N2ASeccEK49tprp/vq7gjp24sASc8IAbJ9Vg7kZ7lggklKZ6lZJ936BAgBklKHqTEESBophw5pnEQhgMDKBPQR1YEAAiUE9JASeuljCZB0ViLrEiBA6vItnr0TCp1YWMSreyZH92yO7vWOd7xjeqfFoYceGv76r/86usTWX8XVBX/5y18OhxxyyHTcZZdddo87Qi6//PKw//7773De7m6SRz/60dOv49p6j9ENNQwgQNJhEyDbZ1XzENfcs8wxwSS1axEgBEhqraTEESAplEJw6JDGSRQCCKxMQB9RHQggUEJADymhlz6WAElnJbIuAQKkLt/i2WsJkJjM2N7G3/72t4fzzz9/8qftSZPbbrstHHXUUeFnP/vZJCbl4epf+tKXwite8Yrpct2+ugeh9+1FgKRnhAAhQFKrhaQgKVJqpWaddOsTIARISh2mxhAgaaQcOqRxEoUAAisT0EdUBwIIlBDQQ0ropY8lQNJZiaxLgACpy7f57KnPALnrrrvCscceG37yk59M9viSl7wk/M7v/M6K++3kRvd1V7fccssk5uUvf3l49atfPRPfPU/k0ksvnfz+yCOPDJ/85Cd3yODFL35x+NrXvjaJ6e4E+chHPtKcWcqCBEgKpZ/HECDbZ1XzENfcs8wxwSS1axEgBEhqraTEESAplNwBkkZJFAII7IiAw0v1gQACJQT0kBJ66WMJkHRWIusSIEDq8m0+e6oA6TbWPVD93HPPneyxe75I9/Dx7T1jZPPmzZMHnl988cWT2N133z184Qtf2O6dGn/7t38bumeNbHl1D1fvpMj2Xh/96EfDGWecMf1T91VfT37yk5szS1mQAEmh9PMYAmT7rBzIz3LBBJOUzlKzTrr1CRACJKUOU2MIkDRSDh3SOIlCAIGVCegjqgMBBEoI6CEl9NLHEiDprETWJUCA1OXbfPYcAbJ+/frwtKc9bfrQ9Pvc5z7hjW98YzjxxBPDrrvuOtn7TTfdFN7ylreE7quqtrxe9apX3eNrqzwApxQAACAASURBVLa9yLVr14bueSBbXi960Ysm8XvuuefkV91zPz7wgQ+Ec845J9x9992T33VfnbXl67WaQ0tYkABJgPSLEAJk+6xqHuKae5Y5Jpikdi0ChABJrZWUOAIkhZI7QNIoiUIAgR0RcHipPhBAoITA/2fv/oMuP8vC/t8Ey+YLNpCQJeSHJasZk8ZATMZRmjZC/dWoIERk1GgMFt2aNqO1KqmGxkYHNY4/Qpsam1qdOCOIGh0RNBQrQqxK68CEDkxSYZJQMEbCrmzJZgP7ZL/zeeKe7D6/7uv+nHPf59yffT3/tLvPdf847+v6XEuut+ccPWQeevG1BEiclci6BAiQunyb714iQIbLvf/970/Dx1A9+uijs7ueeuqp6Qu+4AvSY489lu69997ZF5QPAS95yUvW3zVy0kknbfva9u3bl66++ur04Q9/eBYzvGvk/PPPX1933333rUuQoz9nn312estb3pJ2797dnFf0QAIkSso7QLYjZSBvIB95itRJ2zoZTiNACJDIsxmNIUBipAwdYpxEIYDA9gT0EdWBAALzENBD5qEXX0uAxFmJrEuAAKnLt/nupQJkuOAHPvCB9LrXvS7df//9O9731a9+dbrxxhvTM57xjOzrGiTI8J0iR7/fY7sFl1xySbrlllvS85///OyeywwgQOL0vQNka1YG220H23jjHe1aBAgBEq2VSBwBEqHkHSAxSqIQQGAnAoaX6gMBBOYhoIfMQy++lgCJsxJZlwABUpdv893HCJDhkp/97GfTW9/61vTOd75z/V0fn/zkJ9c/BmsQE8OXkw/y40UvelHx6xkEyNve9rb0vve9L33iE59Ihw8fTs997nPX93rZy162/sXqO72bpPjASgsIkDhYAoQAiVYLSUFSRGqlZp0M5xMgBEikDqMxBEiMlKFDjJMoBBDYnoA+ojoQQGAeAnrIPPTiawmQOCuRdQkQIHX52n0iBAiQeCIJEAIkWi01B9v2JleidUiAECDRWonEESARSt4BEqMkCgEEdiJgeKk+EEBgHgJ6yDz04msJkDgrkXUJECB1+dp9IgQIkHgiCRACJFotJAVJEamVmnUynE+AECCROozGECAxUoYOMU6iEEBgewL6iOpAAIF5COgh89CLryVA4qxE1iVAgNTla/eJECBA4okkQAiQaLXUHGzbm1yJ1iEBQoBEayUSR4BEKHkHSIySKAQQ2ImA4aX6QACBeQjoIfPQi68lQOKsRNYlQIDU5Wv3iRAgQOKJJEAIkGi1kBQkRaRWatbJcD4BQoBE6jAaQ4DESBk6xDiJQgCB7QnoI6oDAQTmIaCHzEMvvpYAibMSWZcAAVKXr90nQoAAiSeSACFAotVSc7Btb3IlWocECAESrZVIHAESoeQdIDFKohBAYCcChpfqAwEE5iGgh8xDL76WAImzElmXAAFSl6/dJ0KAAIknkgAhQKLVQlKQFJFaqVknw/kECAESqcNoDAESI2XoEOMkCgEEtiegj6gOBBCYh4AeMg+9+FoCJM5KZF0CBEhdvnafCAECJJ5IAoQAiVZLzcG2vcmVaB0SIARItFYicQRIhJJ3gMQoiUIAgZ0IGF6qDwQQmIeAHjIPvfhaAiTOSmRdAgRIXb52nwgBAiSeSAKEAIlWC0lBUkRqpWadDOcTIARIpA6jMQRIjJShQ4yTKAQQ2J6APqI6EEBgHgJ6yDz04msJkDgrkXUJECB1+dp9IgQIkHgiCRACJFotNQfb9iZXonVIgBAg0VqJxBEgEUreARKjJAoBBHYiYHipPhBAYB4Cesg89OJrCZA4K5F1CRAgdfnafSIECJB4IgkQAiRaLSQFSRGplZp1MpxPgBAgkTqMxhAgMVKGDjFOohBAYHsC+ojqQACBeQjoIfPQi68lQOKsRNYlQIDU5Wv3iRAgQOKJJEAIkGi11Bxs25tcidYhAUKARGslEkeARCh5B0iMkigEENiJgOGl+kAAgXkI6CHz0IuvJUDirETWJUCA1OVr94kQIEDiiSRACJBotZAUJEWkVmrWyXA+AUKAROowGkOAxEgZOsQ4iUIAge0J6COqAwEE5iGgh8xDL76WAImzElmXAAFSl6/dJ0KAAIknkgAhQKLVUnOwbW9yJVqHBAgBEq2VSBwBEqHkHSAxSqIQQGAnAoaX6gMBBOYhoIfMQy++lgCJsxJZlwABUpev3SdCgACJJ5IAIUCi1UJSkBSRWqlZJ8P5BAgBEqnDaAwBEiNl6BDjJAoBBLYnoI+oDgQQmIeAHjIPvfhaAiTOSmRdAgRIXb52nwgBAiSeSAKEAIlWS83Btr3JlWgdEiAESLRWInEESISSd4DEKIlCAIGdCBheqg8EEJiHgB4yD734WgIkzkpkXQIESF2+dp8IAQIknkgChACJVgtJQVJEaqVmnQznEyAESKQOozEESIyUoUOMkygEENiegD6iOhBAYB4Cesg89OJrCZA4K5F1CRAgdfnafSIECJB4IgkQAiRaLTUH2/YmV6J1SIAQINFaicQRIBFK3gESoyQKAQR2ImB4qT4QQGAeAnrIPPTiawmQOCuRdQkQIHX52n0iBAiQeCIJEAIkWi0kBUkRqZWadTKcT4AQIJE6jMYQIDFShg4xTqIQQGB7AvqI6kAAgXkI6CHz0IuvJUDirETWJUCA1OVr94kQIEDiiSRACJBotdQcbNubXInWIQFCgERrJRJHgEQoeQdIjJIoBBDYiYDhpfpAAIF5COgh89CLryVA4qxE1iVAgNTla/eJECBA4okkQAiQaLWQFCRFpFZq1slwPgFCgETqMBpDgMRIGTrEOIlCAIHtCegjqgMBBOYhoIfMQy++lgCJsxJZlwABUpev3SdCgACJJ5IAIUCi1VJzsG1vciVahyfvuTidddWNs/Db7rwnPfDQgejy9bgXX3RmuvKl52X3GPY9eOhw0d41gnsa0vd01yFXvd33wj2npZuvu3xWZvv3H0yHD6/VKLvj9jR0qI7YAQhMnoA+MvkUe4EIVCWgh1TFO9ucAGnD2Sl5AgRInpEIBBIBEi8CAoQAiVYLSUFSRGqlZp0M52/cP3KnsTHX33p3+tD9+8YuX9i6nob0Pd2VAImXqKFDnJVIBBDYmoA+ojIQQGAeAnrIPPTiawmQOCuRdQkQIHX52n0iBAiQeCIJEAIkWi01B9v2JlfG1mF03Zg4AqScGgFSzqxkhXeAlNASiwACq0TA8HKVsuEuCPRHQA9pkzMCpA1np+QJECB5RiIQ8A6QghogQAiQaLmQFCRFpFZq1slwvneA+A6QSB1GY3oTNgRINLPiEEBg1QgYXq5aRtwHgb4I6CFt8kWAtOHslDwBAiTPSAQCBEhBDRAgBEi0XGoOtu1Nroytw0fuuj09/vCD0eU7xu064wXp9Cv2zmK8A6Qca29Cobf7EiDlNWkFAgisBgHDy9XIg1sg0CsBPaRN5giQNpydkidAgOQZiUCAACmoAQKEAImWC0lBUkRqpWadDOfX3H/XOReks695AwESSfQ2Mb0Jhd7uS4DMUZyWIoDAUgkYXi4Vv8MR6J6AHtImhQRIG85OyRMgQPKMRCBAgBTUAAFCgETLpebg2d7kyirUIQESzcL2cb0Jhd7ue+n5u9NNey+bJeDAgUNpbe2J+ROX2WH4j+FTTjl57nPX1tbSkSPVr+sABBBYQQKGlyuYFFdCoCMCekibZBEgbTg7JU+AAMkzEoEAAVJQAwQIARItF5KCpIjUSs06Gc6vuT8BEsnwzjG9CYXe7zt/xtrusH//wXT48FrbQ52GAAIrQcDwciXS4BIIdEtAD2mTOgKkDWen5AkQIHlGIhAgQApqgAAhQKLlUnPwbG9yZRXqkACJZmH7uN6Fwqp878t2hDfynT9jbXcgQNrydhoCq0TA8HKVsuEuCPRHQA9pkzMCpA1np+QJECB5RiIQIEAKaoAAIUCi5UJSkBSRWqlZJ8P5NfcnQCIZ3jmGAJmf4U47ECB1+dodAQTqETC8rMfWzgicCAT0kDZZJkDacHZKngABkmckAgECpKAGCBACJFouNQfP9iZXVqEOCZBoFraPI0DmZ1giQG678570wEMH6h46x+7nnnlKuvZVF8928A6QOWBaikDnBAwvO0+g6yOwZAJ6SJsEECBtODslT4AAyTMSgQABUlADBAgBEi0XkoKkiNRKzToZzq+5PwESyfDOMQTI/AxLBMiqf2TXhXtOSzdfdzkBUrcs7I5AFwQML7tIk0sisLIE9JA2qSFA2nB2Sp4AAZJnJAIBAqSgBggQAiRaLjUHz/YmV1ahDgmQaBa2jyNA5mdIgNRlaHcEEFgOAcPL5XB3KgJTIaCHtMkkAdKGs1PyBAiQPCMRCBAgBTVAgBAg0XIhKUiKSK3UrJPh/Jr7EyCRDO8cQ4DMz5AAqcvQ7gggsBwChpfL4e5UBKZCQA9pk0kCpA1np+QJECB5RiIQIEAKaoAAIUCi5VJz8GxvcmUV6pAAiWZh+zgCZH6GBEhdhnZHAIHlEDC8XA53pyIwFQJ6SJtMEiBtODslT4AAyTMSgQABUlADBAgBEi0XkoKkiNRKzToZzq+5PwESyfDOMQTI/AwJkLoM7Y4AAsshYHi5HO5ORWAqBPSQNpkkQNpwdkqeAAGSZyQCAQKkoAYIEAIkWi41B8/2JldWoQ4JkGgWto8jQOZnSIDUZWh3BBBYDgHDy+VwdyoCUyGgh7TJJAHShrNT8gQIkDwjEQgQIAU1QIAQINFyISlIikit1KyT4fya+xMgkQzvHEOAzM+QAKnL0O4IILAcAoaXy+HuVASmQkAPaZNJAqQNZ6fkCRAgeUYiECBACmqAACFAouVSc/Bsb3JlFeqQAIlmYfs4AmR+hgRIXYZ2RwCB5RAwvFwOd6ciMBUCekibTBIgbTg7JU+AAMkzEoEAAVJQAwQIARItF5KCpIjUSs06Gc6vuT8BEsnwzjEEyPwMCZC6DO2OAALLIWB4uRzuTkVgKgT0kDaZJEDacHZKngABkmckAgECpKAGCBACJFouNQfP9iZXVqEOCZBoFraPI0DmZ0iA1GVodwQQWA4Bw8vlcHcqAlMhoIe0ySQB0oazU/IECJA8IxEIECAFNUCAECDRciEpSIpIrdSsk+H8mvsTIJEM7xxDgMzPkACpy9DuCCCwHAKGl8vh7lQEpkJAD2mTSQKkDWen5AkQIHlGIhAgQApqgAAhQKLlUnPwbG9yZRXqkACJZmH7OAJkfoYESF2GdkcAgeUQMLxcDnenIjAVAnpIm0wSIG04OyVPgADJMxKBAAFSUAMECAESLReSgqSI1ErNOhnOr7k/ARLJ8M4xBMj8DAmQugztjgACyyFgeLkc7k5FYCoE9JA2mSRA2nB2Sp4AAZJnJAIBAqSgBggQAiRaLjUHz/YmV1ahDgmQaBa2jyNA5mdIgNRlaHcEEFgOAcPL5XB3KgJTIaCHtMkkAdKGs1PyBAiQPCMRCBAgBTVAgBAg0XIhKUiKSK3UrJPh/Jr7EyCRDO8cQ4DMz5AAqcvQ7gggsBwChpfL4e5UBKZCQA9pk0kCpA1np+QJECB5RiIQIEAKaoAAIUCi5VJz8GxvcmUV6pAAiWZh+zgCZH6GBEhdhnZHAIHlEDC8XA53pyIwFQJ6SJtMEiBtODslT4AAyTMSgQABUlADBAgBEi0XkoKkiNRKzToZzq+5PwESyfDOMQTI/AwJkLoM7Y4AAsshYHi5HO5ORWAqBPSQNpkkQNpwdkqeAAGSZyQCAQKkoAYIEAIkWi41B8/2JldWoQ4JkGgWto8jQOZnSIDUZWh3BBBYDgHDy+VwdyoCUyGgh7TJJAHShrNT8gQIkDwjEQgQIAU1QIAQINFyISlIikit1KyT4fya+xMgkQzvHEOAzM+QAKnL0O4IILAcAoaXy+HuVASmQkAPaZNJAqQNZ6fkCRAgeUYiECBACmqAACFAouVSc/Bsb3JlFeqQAIlmYfs4AmR+hgRIXYZ2RwCB5RAwvFwOd6ciMBUCekibTBIgbTg7JU+AAMkzEoEAAVJQAwQIARItF5KCpIjUSs06Gc6vuT8BEsnwzjEEyPwMCZC6DO2OAALLIWB4uRzuTkVgKgT0kDaZJEDacHZKngABkmckAgECpKAGCBACJFouNQfP9iZXVqEOCZBoFraPI0DmZ0iA1GVodwQQWA4Bw8vlcHcqAlMhoIe0ySQB0oazU/IECJA8IxEIECAFNUCAECDRciEpSIpIrdSsk+H8mvsTIJEM7xxDgMzPkACpy9DuCCCwHAKGl8vh7lQEpkJAD2mTSQKkDWen5AkQIHlGIhAgQApqgAAhQKLlUnPwbG9yZRXqkACJZmH7OAJkfoYESF2GdkcAgeUQMLxcDnenIjAVAnpIm0wSIG04OyVPgADJMxKBAAFSUAMECAESLReSgqSI1ErNOhnOr7k/ARLJ8M4xBMj8DAmQugztjgACyyFgeLkc7k5FYCoE9JA2mSRA2nB2Sp4AAZJnJAIBAqSgBggQAiRaLjUHz/YmV1ahDgmQaBa2jyNA5mdIgNRlaHcEEFgOAcPL5XB3KgJTIaCHtMkkAdKGs1PyBAiQPCMRCBAgBTVAgBAg0XIhKUiKSK3UrJPh/Jr7EyCRDO8cQ4DMz5AAqcvQ7gggsBwChpfL4e5UBKZCQA9pk0kCpA1np+QJECB5RiIQIEAKaoAAIUCi5VJz8GxvcmUV6pAAiWZh+zgCZH6GBEhdhnZHAIHlEDC8XA53pyIwFQJ6SJtMEiBtODslT4AAyTMSgQABUlADBAgBEi0XkoKkiNRKzToZzq+5PwESyfDOMQTI/AwJkLoM7Y4AAsshYHi5HO5ORWAqBPSQNpkkQNpwdkqeAAGSZyQCAQKkoAYIEAIkWi41B8/2JldWoQ4JkGgWto8jQOZnSIDUZWh3BBBYDgHDy+VwdyoCUyGgh7TJJAHShrNT8gQIkDwjEQgQIAU1QIAQINFyISlIikit1KyT4fya+xMgkQzvHEOAzM+QAKnL0O4IILAcAoaXy+HuVASmQkAPaZNJAqQNZ6fkCRAgeUYiECBACmqAACFAouVSc/Bsb3JlFeqQAIlmYfs4AmR+hgRIXYZ2RwCB5RAwvFwOd6ciMBUCekibTBIgbTg7JU+AAMkzEoEAAVJQAwQIARItF5KCpIjUSs06Gc6vuf/Jey5OZ1114+xl3nbnPemBhw5EXnZxzLDvwUOHQ+t6kgo93XWA776hEhwddOGe09LN110+W79//8F0+PDa6P0sRACBfgkYXvabOzdHYBUI6CFtskCAtOHslDwBAiTPSAQCBEhBDRAgBEi0XGoOnu1NrqxiHUbvNCbu+lvvTh+6f19oaU9D+p7uSoCEym+uIAJkLnwWIzApAoaXk0qnF4NAcwJ6SBvkBEgbzk7JEyBA8oxEIECAFNQAAUKARMuFpCApIrVSs06G82vuv3HvyOsdG0OAjCW32HWEzWJ5btyNAKnL1+4I9ETA8LKnbLkrAqtHQA9pkxMCpA1np+QJECB5RiIQIEAKaoAAIUCi5dJy8PzxO25Ij3/s3ujVdoxz7+mIGwLkyVyWyJOFPEQFmxAKBbBGhPbGlwAZkWRLEJgoAcPLiSbWy0KgEQE9pA1oAqQNZ6fkCRAgeUYiECBACmqAACFAouVCJExHJPSay9YC5JG7bk+PP/xg9BHZMW7XGS9Ip1+xdxZTIjF6Gnr3dNchGe67kPLedhMCpC5fuyPQEwHDy56y5a4IrB4BPaRNTgiQNpydkidAgOQZiUCAACmoAQKEAImWS69Dc/eejrhpLUAW+U6kXedckM6+5g0ESLThNIojQOqCJkDq8rU7Aj0RMLzsKVvuisDqEdBD2uSEAGnD2Sl5AgRInpEIBAiQghogQAiQaLkQCdMRCb3mkgB5sgZL3j0Sfb4XFUcoLIrk1vv0xvfS83enm/ZeNnsxBw4cSmtrT9SFtKDd19bW0pEjC9rMNgggkAwvFQECCMxDQA+Zh158LQESZyWyLgECpC5fu0+EwL59j3bzH9g55LX/oSdACJBcDR79fa9Dc/eejrghQAiQaL+KxvUmFHq/bzQvqxC3f//BdPjw2ipcxR0QmASB2v9NMwlIXgQCCGxLQA9pUxwESBvOTskTIEDyjEQg4B0gBTVAgBAg0XIhEqYjEnrNJQFCgET7VTSud6Gwyu8GGnKwkW80L6sQR4CsQhbcYUoEDC+nlE2vBYH2BPSQNswJkDacnZInQIDkGYlAgAApqAEChACJlkuvQ3P3no64IUAIkGi/isYRIFFS4+IIkHHcrEJgigQML6eYVa8JgXYE9JA2rAmQNpydkidAgOQZiUCAACmoAQKEAImWC5EwHZHQay4JEAIk2q+icQRIlNS4uI18b7vznvTAQwfGbVZ51blnnpKufdXFs1O8A6QycNufcAQML0+4lHvBCCyUgB6yUJzbbkaAtOHslDwBAiTPSAQCBEhBDRAgBEi0XHodmrv3dMQNAUKARPtVNI4AiZIaF9cT3wv3nJZuvu5yAmRcqq1CIEvA8DKLSAACCOxAQA9pUx4ESBvOTskTIEDyjEQgQIAU1AABQoBEy4VImI5I6DWXBAgBEu1X0bieBvTDa3LfaGbL4wiQcmZWIFBCwPCyhJZYBBDYSEAPaVMTBEgbzk7JEyBA8oxEIECAFNQAAUKARMul16G5e09H3BAgBEi0X0XjCIUoqXFxPfElQMbl2CoEogQML6OkxCGAwFYE9JA2dUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XIiE6YiEXnNJgBAg0X4VjetpQD+8JveNZrY8jgApZ2YFAiUEDC9LaIlFAIGNBPSQNjVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFx6HZq793TEDQFCgET7VTSOUIiSGhfXE18CZFyOrUIgSsDwMkpKHAIIbEVAD2lTFwRIG85OyRMgQPKMRCBAgBTUAAFCgETLhUiYjkjoNZcECAES7VfRuJ4G9MNrct9oZsvjCJByZlYgUELA8LKEllgEENhIQA9pUxMESBvOTskTIEDyjEQgQIAU1AABQoBEy6XXobl7T0fcECAESLRfReMIhSipcXE98SVAxuXYKgSiBAwvo6TEIYDAVgT0kDZ1QYC04eyUPAECJM9IBAIESEENECAESLRciITpiIRec0mAECDRfhWN62lAP7wm941mtjyOAClnZgUCJQQML0toiUUAgY0E9JA2NUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XHodmrv3dMQNAUKARPtVNI5QiJIaF9cTXwJkXI6tQiBKwPAySkocAghsRUAPaVMXBEgbzk7JEyBA8oxEIECAFNQAAUKARMuFSJiOSOg1lwQIARLtV9G4ngb0w2ty32hmy+MIkHJmViBQQsDwsoSWWAQQ2EhAD2lTEwRIG85OyRMgQPKMRCBAgBTUAAFCgETLpdehuXtPR9wQIARItF9F4wiFKKlxcT3xJUDG5dgqBKIEDC+jpMQhgMBWBPSQNnVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFyIhOmIhF5zSYAQINF+FY3raUA/vCb3jWa2PI4AKWdmBQIlBAwvS2iJRQCBjQT0kDY1QYC04eyUPAECJM9IBAIESEENECAESLRceh2au/d0xA0BQoBE+1U0jlCIkhoX1xNfAmRcjq1CIErA8DJKShwCCGxFQA9pUxcESBvOTskTIEDyjEQgQIAU1AABQoBEy4VImI5I6DWXBAgBEu1X0bieBvTDa3LfaGbL4wiQcmZWIFBCwPCyhJZYBBDYSEAPaVMTBEgbzk7JEyBA8oxEIECAFNQAAUKARMul16G5e09H3BAgBEi0X0XjCIUoqXFxPfElQMbl2CoEogQML6OkxCGAwFYE9JA2dUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XIiE6YiEXnNJgBAg0X4VjetpQD+8JveNZrY8jgApZ2YFAiUEDC9LaIlFAIGNBPSQNjVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFx6HZq793TEDQFCgET7VTSOUIiSGhfXE18CZFyOrUIgSsDwMkpKHAIIbEVAD2lTFwRIG85OyRMgQPKMRCBAgBTUAAFCgETLhUiYjkjoNZcECAES7VfRuJ4G9MNrct9oZsvjCJByZlYgUELA8LKEllgEENhIQA9pUxMESBvOTskTIEDyjEQgQIAU1AABQoBEy6XXobl7T0fcECAESLRfReMIhSipcXE98SVAxuXYKgSiBAwvo6TEIYDAVgT0kDZ1QYC04eyUPAECJM9IBAIESEENECAESLRciITpiIRec0mAECDRfhWN62lAP7wm941mtjyOAClnZgUCJQQML0toiUUAgY0E9JA2NUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XHodmrv3dMQNAUKARPtVNI5QiJIaF9cTXwJkXI6tQiBKwPAySkocAghsRUAPaVMXBEgbzk7JEyBA8oxEIECAFNQAAUKARMuFSJiOSOg1lwQIARLtV9G4ngb0w2ty32hmy+MIkHJmViBQQsDwsoSWWAQQ2EhAD2lTEwRIG85OyRMgQPKMRCBAgBTUAAFCgETLpdehuXtPR9wQIARItF9F4wiFKKlxcT3xJUDG5dgqBKIEDC+jpMQhgMBWBPSQNnVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFyIhOmIhF5zSYAQINF+FY3raUA/vCb3jWa2PI4AKWdmBQIlBAwvS2iJRQCBjQT0kDY1QYC04eyUPAECJM9IBAIESEENECAESLRceh2au/d0xA0BQoBE+1U0jlCIkhoX1xNfAmRcjq1CIErA8DJKShwCCGxFQA9pUxcESBvOTskTIEDyjEQgQIAU1AABQoBEy4VImI5I6DWXBAgBEu1X0bieBvTDa3LfaGbL4wiQcmZWIFBCwPCyhJZYBBDYSEAPaVMTBEgbzk7JEyBABB/tqQAAIABJREFU8oxEIECAFNQAAUKARMul16G5e09H3BAgBEi0X0XjCIUoqXFxPfElQMbl2CoEogQML6OkxCGAwFYE9JA2dUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XIiE6YiEXnNJgBAg0X4VjetpQD+8JveNZrY8jgApZ2YFAiUEDC9LaIlFAIGNBPSQNjVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFx6HZq793TEDQFCgET7VTSOUIiSGhfXE18CZFyOrUIgSsDwMkpKHAIIbEVAD2lTFwRIG85OyRMgQPKMRCBAgBTUAAFCgETLhUiYjkjoNZcECAES7VfRuJ4G9MNrct9oZsvjCJByZlYgUELA8LKEllgEENhIQA9pUxMESBvOTskTIEDyjEQgQIAU1AABQoBEy6XXobl7T0fcECAESLRfReMIhSipcXE98SVAxuXYKgSiBAwvo6TEIYDAVgT0kDZ1QYC04eyUPAECJM9IBAIESEENECAESLRciITpiIRec0mAECDRfhWN62lAP7wm941mtjyOAClnZgUCJQQML0toiUUAgY0E9JA2NUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XHodmrv3dMQNAUKARPtVNI5QiJIaF9cTXwJkXI6tQiBKwPAySkocAghsRUAPaVMXBEgbzk7JEyBA8oxEIECAFNQAAUKARMuFSJiOSOg1lwQIARLtV9G4ngb0w2ty32hmy+MIkHJmViBQQsDwsoSWWAQQ2EhAD2lTEwRIG85OyRMgQPKMRCBAgBTUAAFCgETLpdehuXtPR9wQIARItF9F4wiFKKlxcT3xJUDG5dgqBKIEDC+jpMQhgMBWBPSQNnVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFyIhOmIhF5zSYAQINF+FY3raUA/vCb3jWa2PI4AKWdmBQIlBAwvS2iJRQCBjQT0kDY1QYC04eyUPAECJM9IBAIESEENECAESLRceh2au/d0xA0BQoBE+1U0jlCIkhoX1xNfAmRcjq1CIErA8DJKShwCCGxFQA9pUxcESBvOTskTIEDyjEQgQIAU1AABQoBEy4VImI5I6DWXBAgBEu1X0bieBvTDa3LfaGbL4wiQcmZWIFBCwPCyhJZYBBDYSEAPaVMTBEgbzk7JEyBA8oxEIECAFNQAAUKARMul16G5e09H3BAgBEi0X0XjCIUoqXFxPfElQMbl2CoEogQML6OkxCGAwFYE9JA2dUGAtOHslDwBAiTPSAQCBEhBDRAgBEi0XIiE6YiEXnNJgBAg0X4VjetpQD+8JveNZrY8jgApZ2YFAiUEDC9LaIlFAIGNBPSQNjVBgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFx6HZq793TEDQFCgET7VTSOUIiSGhfXE99Lz9+dbtp72eyFHjhwKK2tPTHuhS9h1draWjpyZAkHOxKBIAHDyyAoYQggsCUBPaRNYRAgbTg7JU+AAMkzEoEAAVJQAwQIARItFyJhOiKh11wSIARItF9F43oa0A+vyX2jmS2P28i2fIflrti//2A6fHhtuZdwOgI7EDC8VB4IIDAPAT1kHnrxtQRInJXIugQIkLp87T4RAvv2PdrV/9XeTthr/0NPgBAg0ce+16G5e09H3BAgBEi0X0XjCIUoqXFxPfElQMbl2CoEogRq/zdN9B7iEECgTwJ6SJu8ESBtODslT4AAyTMSgYB3gBTUAAFCgETLhUiYjkjoNZcECAES7VfRuJ4G9MNrct9oZsvjCJByZlYgUELA8LKEllgEENhIQA9pUxMESBvOTskTIEDyjEQgQIAU1AABQoBEy6XXobl7T0fcECAESLRfReMIhSipcXE98d1419vuvCc98NCBcS+8wapzzzwlXfuqi2cn+QisBtAdMRcBw8u58FmMwAlPQA9pUwIESBvOTskTIEDyjEQgQIAU1AABQoBEy4VImI5I6DWXBAgBEu1X0bieBvTDa3LfaGbL43pje+Ge09LN111OgJSn2oolETC8XBJ4xyIwEQJ6SJtEEiBtODslT4AAyTMSgQABUlADBAgBEi2XXofm7j0dcUOAECDRfhWN623o7b7RzJbH9caWACnPsRXLJWB4uVz+TkegdwJ6SJsMEiBtODslT4AAyTMSgQABUlADBAgBEi0XImE6IqHXXBIgBEi0X0Xjeht6u280s+VxvbElQMpzbMVyCRheLpe/0xHonYAe0iaDBEgbzk7JEyBA8oxEIECAFNQAAUKARMul16G5e09H3BAgBEi0X0Xjeht6u280s+VxvbElQMpzbMVyCRheLpe/0xHonYAe0iaDBEgbzk7JEyBA8oxEIECAFNQAAUKARMuFSJiOSOg1lwQIARLtV9G43obe7hvNbHlcb2wJkPIcW7FcAoaXy+XvdAR6J6CHtMkgAdKGs1PyBAiQPCMRCBAgBTVAgBAg0XLpdWju3tMRNwQIARLtV9G43obe7hvNbHlcb2wJkPIcW7FcAoaXy+XvdAR6J6CHtMkgAdKGs1PyBAiQPCMRCBAgBTVAgBAg0XIhEqYjEnrNJQFCgET7VTSut6G3+0YzWx7XG1sCpDzHViyXgOHlcvk7HYHeCeghbTJIgLTh7JQ8AQIkz0gEAgRIQQ0QIARItFx6HZq793TETc8C5OQ9F6ezrrpxlozb7rwnPfDQgdDj9+KLzkxXvvS88Nph34OHDof2XnRQb0Nk9110BRy/X098e7rrQJkAqVu7dl88AcPLxTO1IwInEgE9pE22CZA2nJ2SJ0CA5BmJQIAAKagBAoQAiZYLkTAdkdBrLnsWIBuZR5+7MXHX33p3+tD9+8YsnXtNb0Nk95075Ttu0BPfnu5KgNStW7vXIWB4WYerXRE4UQjoIW0yTYC04eyUPAECJM9IBAIESEENECAESLRceh2au/d0xA0BEntaCZAYpyGqt6G3+8ZzWxrZG1vvACnNsPhlEzC8XHYGnI9A3wT0kDb5I0DacHZKngABkmckAgECpKAGCBACJFouRMJ0REKvuSRAYk8rARLjRIDEOY2N7Ekq9HTXIR8EyNiqtG5ZBAwvl0XeuQhMg4Ae0iaPBEgbzk7JEyBA8oxEIECAFNQAAUKARMul16G5e09H3ExJgDxy1+3p8YcfjD5+O8btOuMF6fQr9s5iCJA41t6G3u4bz21pZG9sCZDSDItfNgHDy2VnwPkI9E1AD2mTPwKkDWen5AkQIHlGIhAgQApqgAAhQKLlQiRMRyT0msspCZCP33FDevxj90Yfv50FyDkXpLOveQMBMoJmb0Nv9x2R5OCS3tgSIMHEClsZAoaXK5MKF0GgSwJ6SJu0ESBtODslT4AAyTMSgQABUlADBAgBEi2XXofm7j0dcUOAbP207iJAom1sU1xvQ2/3HZ3q7MLe2BIg2ZQKWDEChpcrlhDXQaAzAnpIm4QRIG04OyVPgADJMxKBAAFSUAMECAESLRciYToioddcEiAESLRfReN6G3q7bzSz5XG9sSVAynNsxXIJGF4ul7/TEeidgB7SJoMESBvOTskTIEDyjEQgQIAU1AABQoBEy6XXobl7T0fcECAESLRfReN6G3q7bzSz5XG9sSVAynNsxXIJGF4ul7/TEeidgB7SJoMESBvOTskTIEDyjEQgQIAU1AABQoBEy4VImI5I6DWXBAgBEu1X0bjeht7uG81seVxvbAmQ8hxbsVwChpfL5e90BHonoIe0ySAB0oazU/IECJA8IxEIECAFNUCAECDRcul1aO7e0xE3BAgBEu1X0bjeht7uG81seVxvbAmQ8hxbsVwChpfL5e90BHonoIe0ySAB0oazU/IECJA8IxEIECAFNUCAECDRciESpiMSes0lAUKARPtVNK63obf7RjNbHtcbWwKkPMdWLJeA4eVy+Tsdgd4J6CFtMkiAtOHslDwBAiTPSAQCBEhBDRAgBEi0XHodmrv3dMQNAUKARPtVNK63obf7RjNbHtcbWwKkPMdWLJeA4eVy+Tsdgd4J6CFtMkiAtOHslDwBAiTPSAQCBEhBDRAgBEi0XIiE6YiEXnNJgBAg0X4Vjett6O2+0cyWx/XGlgApz7EVyyVgeLlc/k5HoHcCekibDBIgbTg7JU+AAMkzEoEAAVJQAwQIARItl16H5u49HXFDgBAg0X4Vjett6O2+0cyWx/XGlgApz7EVyyVgeLlc/k5HoHcCekibDBIgbTg7JU+AAMkzEoEAAVJQAwQIARItFyJhOiKh11wSIARItF9F43obertvNLPlcb2xJUDKc2zFcgkYXi6Xv9MR6J2AHtImgwRIG85OyRMgQPKMRCBAgBTUAAFCgETLpdehuXtPR9wQIARItF9F43obertvNLPlcb2xJUDKc2zFcgkYXi6Xv9MR6J2AHtImgwRIG85OyRMgQPKMRCBAgBTUAAFCgETLhUiYjkjoNZcECAES7VfRuN6G3u4bzWx5XG9sCZDyHFuxXAKGl8vl73QEeiegh7TJIAHShrNT8gQIkDwjEQgQIAU1QIAQINFy6XVo7t7TETcECAES7VfRuN6G3u4bzWx5XG9sCZDyHFuxXAKGl8vl73QEeiegh7TJIAHShrNT8gQIkDwjEQgQIAU1QIAQINFyIRKmIxJ6zSUBQoBE+1U0rreht/tGM1se1xtbAqQ8x1Ysl4Dh5XL5Ox2B3gnoIW0ySIC04eyUPAECJM9IBAIESEENECAESLRceh2au/d0xA0BQoBE+1U0rreht/tGM1se1xtbAqQ8x1Ysl4Dh5XL5Ox2B3gnoIW0ySIC04eyUPAECJM9IBAIESEENECAESLRciITpiIRec0mAECDRfhWN623o7b7RzJbH9caWACnPsRXLJWB4uVz+TkegdwJ6SJsMEiBtODslT4AAyTMSgQABUlADBAgBEi2XXofm7j0dcUOAECDRfhWN623o7b7RzJbH9caWACnPsRXLJWB4uVz+TkegdwJ6SJsMEiBtODslT4AAyTMSgQABUlADBAgBEi0XImE6IqHXXBIgBEi0X0Xjeht6u280s+VxvbElQMpzbMVyCRheLpe/0xHonYAe0iaDBEgbzk7JEyBA8oxWLuJ//+//nX73d383vf/9708f//jH06c//el08sknp9NPPz1dcskl6au+6qvSV3zFV6SnPe1pobt/5jOfSW9/+9vTXXfdlT74wQ+mv/3bv03Petaz0hlnnJEuu+yydOWVV6bzzz8/tNexQX/6p3+afud3fmf9np/4xCfSSSedtL7nC1/4wvQN3/AN6fLLLy/ec1kL9u17NK2tPbGs4xd6bu1/6AkQAiRasL0Ozd17OuKGACFAov0qGtfb0Nt9o5ktj+uNLQFSnmMrlkug9n/TLPfVOR0BBGoT0ENqE35yfwKkDWen5AkQIHlGKxMxSITXv/716Y//+I+zdxqExc/93M+l8847b8fYe++9N/2bf/Nv0kc+8pFt4wZx8ZrXvCZ9//d/f3rGM56RPftTn/pUuv7669O73vWuHWMHAfITP/ET6XnPe152z2UHECDxDBAgW7MyNN/MBRNMIp2lZp0M59fcv9e9d51zQTr7mjfM0nP9rXenD92/L5Kuhcf0NkR234WXwHEb9sS3p7sOkAmQurVr98UTMLxcPFM7InAiEdBD2mSbAGnD2Sl5AgRIntFKRPz1X/91+tZv/db0V3/1V7P7DGJiEBynnXZa+n//7/+l//N//k/67Gc/O/v9M5/5zHTHHXekF73oRVu+hkF+XH311enAgQOz3+/evTvt2bNn/e+G/Z544ql3PVxxxRXplltu2fGdJcO7Ua666qp03333zfYc3k3yhV/4het7/eVf/mU6ePDg7Hfnnntuestb3pKe85znrATn7S5BgMTTQ4BszarXQah7kxSRp7/XOiFAts4uARKp+q1jeht6u+/4XOdW9saWAMll1O9XjYDh5aplxH0Q6IuAHtImXwRIG85OyRMgQPKMlh5x5MiR9M3f/M3pnnvumd1lEBfXXntteu5znzv7u0cffTT96q/+avpP/+k/zUTI8LFYv//7v5+e/exnH/c6Dh06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iSemfffdt6LP2LFj05FHHlnO98gjj6SVV165YrmFmUEApHrtBTlIJAAy935YkOau/e0O+gkKLdigp2eKZ0q1/3fzLPx2n4Xv3XlZ+s/UKdV2V8V8S7ZZK62yU79yPgEQA50VvzSNyFBPg5wGvRvR0VUU9V2oAqkRWfg2Aq9C0XoPgMxtxUoMzC+//FLllhdpVcvcVqwsuN5dsFcWAFmwvq5evYAASPVWclYQmDJlSuratWs5V2yF1aVLl4pukyZNSj169Cjnu+6661KnTp0qlluYGQRAqtdekINEBisNVlb7TVyQ30PX/nYHQpsyKOSZ4pnimVKtQPP6d79k+45pjf1OLzdKAEQAJP+/hMolDcpWNmpMjnryrae6Rp+ob2O+mZXL1pNvvQdAKvdGsXI0h0PmS6ICIMX6brXk2giAtOTeb+K2T5gwIfXt27d81ZEjR6Z11lmn4l2mTp2attlmm3K+Cy64IO28884Vyy3MDNOnf5q++uqbhXnLBXav+B9Q69ZLN7j+1FEXpi+mvtYk91x2nc5ppa3/e7B9U147Krggr+/ac34FmDCp5sFQr98Tz5S592699qd6e15V87yKPEu0+W5q87MjytnPu+7J9Mq/pldbvKp822y0Ruq1ww8X6D2qqkiVmdS3Sqgc2djmQKuhSD351lNdowvUt4YvYo6s9eQ7e11H3PVC+te7M3K0euEU2fD/rZq233TNhXOzBXCX6dM/q6szVuZHsOiii6TWrZdZAEouSaA2AQGQ2rzkno/AXXfdlfr371/Occ8996T27dtXNJsxY0aDFR9DhgxJvXr1qlhOBgIECBAgQIAAAQIECBAgQIAAAQIECBAgMC8BARDfjSYTGDNmTBowYED5eg8//HBaZZVVKl5/5syZaf311y/nq/bskIoXloEAAQIECBAgQIAAAQIECBAgQIAAAQIEWqyAAEiL7fqmb3hseXXccceVLzx+/Pi00korVbzRN998kzp27FjOd/zxx6cDDjigYjkZCBAgQIAAAQIECBAgQIAAAQIECBAgQIDAvAQEQHw3mkxg9OjRaeDAgeXr5V0BcvLJJzc4S6TJKuhCBAgQIECAAAECBAgQIECAAAECBAgQINBiBARAWkxXL/iGzn4GyL333pvWWGONijee/QyQ0047Le25538P0a54ARkIECBAgAABAgQIECBAgAABAgQIECBAgMBsAgIgvhJNJjBhwoQGKzdGjRrVYGured3o7bffTl26dCl/PGzYsLTDDjs0Wb1ciAABAgQIECBAgAABAgQIECBAgAABAgRanoAASMvr8wXW4ilTpqSuXbuWrz98+PDUuXPnivd79tlnU8+ePcv5RowYkTbaaKOK5WQgQIAAAQIECBAgQIAAAQIECBAgQIAAAQLzEhAA8d1oMoGZM2emjTfeOMV/Iw0ePDjtvffeFa9/xx13pKOOOqqc7/HHH0+tW7euWE4GAgQIECBAgAABAgQIECBAgAABAgQIECAgAOI7sFAEYiVHrOiI1KtXrzRkyJCK9z333HPT5ZdfnuWLM0Pi7BCJAAECBAgQIECAyZu4QQAAIABJREFUAAECBAgQIECAAAECBAg0RsAKkMboKTuHQJ5gRvfu3dNzzz2XXWuvvfZKQ4cOJUuAAAECBAgQIECAAAECBAgQIECAAAECBBolIADSKD6FZxeYNGlS6tGjR/mvL7vssgYHnM+ef+LEial3797lv77yyivTFltsAZYAAQIECBAgQIAAAQIECBAgQIAAAQIECDRKQACkUXwKz00gAhoR2IgUW1rdcMMNabXVVpsj6/Tp07Pgx6uvvpp91rFjxzRq1CioBAgQIECAAAECBAgQIECAAAECBAgQIECg0QICII0mdIHZBSL40adPn/TVV19lH6255prp9NNPT5tttlk56zPPPJMGDRqUXnrppezvWrVqla666qoGecgSIECAAAECBAgQIECAAAECBAgQIECAAIG8AgIgeeWUm6/ANddcM8dZHu3bt0/t2rVL77zzTnr99dcblB8wYEDq168fVQIECBAgQIAAAQIECBAgQIAAAQIECBAg0CQCAiBNwugicxMYOXJktvLjo48+mifQUkstlY499thsxYhEgAABAgQIECBAgAABAgQIECBAgAABAgSaSkAApKkkXWeuAtOmTUs333xzuu+++9Ibb7yRPvzww7T00kunDh06pM6dO2dngLRt25YeAQIECBAgQIAAAQIECBAgQIAAAQIECBBoUgEBkCbldDECBAgQIECAAAECBAgQIECAAAECBAgQIECgCAICIEXoBXUgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEmlRAAKRJOV2MAAECBAgQIECAAAECBAgQIECAAAECBAgQKIKAAEgRekEdCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgSYVEABpUk4XI0CAAAECBAgQIECAAAECBAgQIECAAAECBIogIABShF5QBwIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBJBQRAmpTTxQgQIECAAAECBAgQIECAAAECBAgQIECAAIEiCAiAFKEX1IEAAQIECBAgQIAAAQIECBAgQIAAAQIECBBoUgEBkCbldDECBAgQIECAAAECBAgQIECAAAECBAgQIECgCAICIEXoBXUgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEmlRAAKRJOV2MAAECBAgQIECAAAECBAgQIECAAAECBAgQKIKAAEgRekEdCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgSYVEABpUk4XI0CAAAECBAgQIECAAAECBAgQIECAAAECBIogIABShF5QBwIECBAgQIAAAQIECBAgQIAAAQIECBAgQKBJBQRAmpTTxQgQIECAAAECBAgQIECAAAECBAgQIECAAIEiCAiAFKEX1IEAAQIECBAgQIAAAQIECBAgQIAAAQIECBBoUgEBkCbldDECBAgQIECAAAECBAgQIECAAAECBAgQIECgCAICIEXoBXUgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEmlRAAKRJOV2MAAECBAgQIECAAAECBAgQIECAAAECBAgQKIKAAEgRekEdCCwEgWnTpqWbbrop3X///emVV15Jn3zySVphhRVS+/bt03bbbZe6d++eVl111YVQE7cgQKCeBOKZ0a9fv5qrfMIJJ6T999+/5nIKECBQ/wITJ05Mv/jFL9I333yTrr766rT55ptX3agvvvgi3X777enOO+9MkydPTh9++GFadtllU5s2bdKWW26Z9thjj/TDH/6w6uvJSIBAfQrkeY58+umnqVOnTunrr7+uqdHxW+jiiy+uqYzMBAgUR+DZZ59No0aNSvHc+Ne//pVmzJiRllpqqbTKKqukjTfeOG2//fbppz/9aVpkkUWqqrR3kaqYZCJQVwICIHXVXSpLIJ/A2LFj0+DBg9P06dPneYHlllsunXjiiennP/95vpsoRYBAsxS49NJL03nnnVdz2wRAaiZTgECzEIhBhx49eqTXX389a08tAZDnn38+HX300dlEjXmlVq1aZcHVo446Ki2xxBLNwkwjCBBoKJD3ORKDn717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FclkINBsBSZPnpxiK71S6ty5czaIML/0ne98J1tCLnDabL8WGkagokAtAZBvvvkmrb/++uUD1GMwdP/99694j8gQEz1iwkekvffeOw0ePLiqcjIRIFB8gVqeI6XWbLLJJunjjz/O/hjB2aeffrp8IPrcWhwzxgcOHGh1a/G/DmpIoNECsdI0VnmUUgRIzz777OyP3kUazesCBOpCQACkLrpJJQnUJnDXXXel/v37lwvdc889qX379hUvEstIZx24HDJkSOrVq1fFcjIQIND8BOJg0tg+b/YUB4rGljcxc+q9995Lr776avbDoZRiBcg555xjO5rm95XQIgJVCdQycDl9+vRsoLKUzjjjjAaB1/ndcNazzmL1WRzILhEg0DwEanmORItjVWqsRJ09xezueGdZddVVU/zOefHFF8srW0t5Y1B00KBBzQNOKwgQmEPggw8+SD179sy26IzUqlWr7Mygjh07Zn/2LuJLQ6BlCAiAtIx+1soWJjBmzJhs6XcpxaztVVZZpaJCbHUTMzFLqdqzQypeWAYCBOpOYOjQoemaa64p13v55ZfPnitx6OAyyyxT/vtYORbb7M2ad8kll0zXXntt2mCDDequ3SpMgEDjBGoZuHznnXeyrWhK6fzzzy+fJVKpFnEm0cSJE7Ns1Z4dUumaPidAoBgCtTxHosbjxo1Lhx9+eLnyMcB5wAEHZDO+43yAUvrss8/STTfdlOJZU9pCLz47+eSTG6yeL4aCWhAg0FiBzz//PNte84knnihfKt4f4mzDUvIu0lhl5QnUh4AASH30k1oSqEkgtrw67rjjymVif8vYp79SilncpZkQkff444/PfjxIBAi0PIH4t//II49kDY/BgzgTaH4ryWJA4aSTTipDxf78N9xwQ8uD02ICLVygloHLt956K/3kJz8pi1144YVpp512qkpw1v3+4xp//OMfqyonEwECxReo5TkSrbnkkktSbN0bKc4kuvjii1OXLl3m2dDnnnsu9enTJzsXJNKyyy6b7r777qp+LxVfTw0JEAiBCHjG+WAxFlJKcW7h9ddfn2KyVil5F/F9IdAyBARAWkY/a2ULExg9enS2p20p5V0BYjZUC/viaC6B2QSmTZuWLRdfccUVU5zvUSkdddRR6Y477ihniwBIBEIkAgRajkAtA5eznz2WdwXIjjvumH7/+9+3HGQtJdDMBWp5jpQoIpgR5b788ssUg5yVUgyCnnLKKeVsRx99dPrVr35VqZjPCRCoA4HY9iqCH6WVolHldu3aZRO62rZt26AF3kXqoENVkUATCAiANAGiSxAomsDsZ4Dce++9aY011qhYzdnPADnttNPSnnvuWbGcDAQIEAiB+JERy8pL6bDDDmuwJQUlAgSav0AtA5ez77t95plnpj322KMqpFnPAOnWrVs699xzqyonEwECxReo5TmStzVffPFF2nzzzctbYW266aYNtvPMe13lCBD4dgWmTJmSBTNfe+21ckUi+HHVVVelNddcc47KeRf5dvvL3QksLAEBkIUl7T4EFqLAhAkTGuxjO2rUqAZbW82rKm+//XaD5eLDhg3L9tWWCBAgUI1AzLrcaKONygeM7rrrrum8886rpqg8BAg0E4FaBi5j682Yqf3VV19lra/l7LF4P3njjTeycvvss0+DLfiaCaVmEGixArU8RxqDFGeEPProo9kl4qD0hx56qDGXU5YAgW9ZIP49H3HEEenDDz8s12TttddOf/7zn7MVIHNL3kW+5U5zewILSUAAZCFBuw2BhSkQsx66du1avuXw4cNT586dK1bh2WefTT179iznGzFiRDaYKREgQKBaga222iq9++67WfZ47sTzRyJAoOUI1Dpwuc0226TYfiLSIYcckmIrvWpSbK9XOsR4wIABqV+/ftUUk4cAgToQqPU5krdJ8ewYM2ZMVnzxxRdPkyZNynsp5QgQ+JYFYuvdoUOHZtvglVKMZcQZYbGd7/ySd5FvufPcnsBCEBAAWQjIbkFgYQvMnDkz23c//htp8ODBae+9965Yjdi7f9aBh8cffzy1bt26YjkZCBAgUBLYbLPNUiwljxSB2D/84Q9wCBBoQQK1Dlzuu+++6bHHHsuEdt555/JBxvMje//999OWW25ZznLRRRel7bffvgUpayqB5i1Q63Mkr0b//v1TbB0caYUVVig/i/JeTzkCBBa+QKzgOOuss9IVV1zR4OZxPtjZZ5+dllpqqYqV8i5SkUgGAnUvIABS912oAQTmLhArOWJFR6RevXqlIUOGVKSK/bMvv/zyLF+cGRJnh0gECLQ8gcmTJ6fRo0enOAQ9DhGMQ0Lbt29fESKWm//4xz9O8UMk0v77759OOOGEiuVkIECg+QjUOnAZgxOxNUWkDh06pHHjxlXEeOCBB9LBBx9cznfPPfdU9YyqeGEZCBAohEAtz5F494jfL6V3lvgNVG1AdPfdd08vvPBC1uZ111033XrrrYVov0oQIFCdQGyhGb81YsvvWVO8I8QKr0UWWaSqC3kXqYpJJgJ1LSAAUtfdp/IE5i2QJ5jRvXv39Nxzz2UX3WuvvbIlpBIBAi1PYPz48VnwopROO+20tOeee1aEuO2229IxxxxTzmdWdkUyGQg0O4FaBi6j8XmCGb/97W+zw0wjVRs0aXbQGkSgGQvU8hyJw8xj5Xtp25sIapxzzjkVdeLsw2233bY8aSNmgMc5RBIBAvUhEBOujj322GzSVikttthi2cStan63zNpK7yL10edqSaAxAgIgjdFTlkCBBWIP2x49epRreNlllzU44Hz2qk+cODH17t27/NdXXnll2mKLLQrcQlUjQGBBCXzyySfZ+R2fffZZdosNNtgg3XTTTfOdRRVb7sUzpzSTcuWVV0733XdfWnLJJRdUNV2XAIECCtQycBnVj8HLrbfeunxg6UEHHZQGDhw4z5bNmDEjm90dq9Mi/frXv84OPJUIEGg+ArU+R/r27ZsmTJiQASy99NIpVoXFe8j8UgySXn/99eUst9xyS1pvvfWaD6KWEGjmArHN7rBhw8qtXGaZZdKFF16Y4jyPWpN3kVrF5CdQfwICIPXXZ2pMoGqBCGhEYCNSbGkVB4Otttpqc5SP/foj76uvvpp91rFjxzmWkVZ9UxkJEGgWAieddFIW9Cil4447Lv3yl7+ca9tiBlacNTRixIjy5zEj68ADD2wWFhpBgED1ArUOXMaVzz///OyQ0khxEHFsibX55pvPcdN41sSWFrfffnv2Wezr/be//S21adOm+grKSYBA4QVqfY7EDPBZA6fbbbddNjDaqlWrubY1tsuJ95RSipUgl156aeFdVJAAgf8ViLPDYrX6119/nf05JlwNHz48bbLJJrmJvIvkplOQQF0ICIDURTepJIF8AhH86NOnT4q9MSOtueaa6fTTT09xSHEpPfPMM2nQoEHppZdeyv4qfijEthKz5sl3d6UIEKhngffeey/tuuuu5VnZsYfufvvtlw499NDsoNBSeuWVV9KZZ56ZbWNTSp06dUp/+ctf0qKLLlrPBOpOgEAOgVoHLuMWH330Ufa8eeedd7I7xizOeDfZY489UmxnEWnq1KnZeWZ33313uVaHH354Ouyww3LUUhECBIosUOtzJIKj8ZvnySefLDdrq622yra0Wnvttct/F+eExHkhcVhy6byyeKeJAIpAapG/EepG4L8C8W+3W7du5fGL+CQOQY/tvBuTvIs0Rk9ZAsUXEAApfh+pIYFGCVxzzTVznOURhxm3a9cuG2h4/fXXG1w/Zlb269evUfdUmACB5iHw1FNPZas4Pv3003KDYnb2D37wg7TccstlA5KzP0M23HDDbPb28ssv3zwQtIIAgZoEah24LF08Jm3E8ya24CulFVdcMX3ve9/LtuN7/vnnyxM64vMuXbpkq0bmNcO7pkrLTIBAoQTyPEfef//9LAjy2muvNWhLBEBiBXyseH/xxRcbPEfiGRPb/sbqd4kAgfoQuPPOOxtsfRm/Tea2arRSa2LV2Oz/9r2LVFLzOYH6FRAAqd++U3MCVQuMHDkyW/kRsxrmlWIbiVgKHj8cJAIECJQEXn755ezZMHny5PmixGqP2Erv6KOPzoIjEgECLVMgz8BlSSpWpcbzZvYBzNkl43DT//mf/0lLLLFEy0TWagLNXCDvcySCHKeeemp5m7z5McUKkXiOrLXWWs1cU/MINC+BWP05bty4Rjfq6quvnmvgxLtIo2ldgEAhBQRACtktKkWg6QViyffNN9+cHUr8xhtvZNvaxCGBHTp0yA47joHLtm3bNv2NXZEAgboXiKXmDz74YBo7dmx6+umns9Vj//nPf7KtsOJ8oRhE2GWXXbKZ2hIBAi1bIO/AZUlt5syZ2XY0d911V7bqI2Z1xzZYq6++era3dwQ/YqWZRIBA8xVo7HMkVnrEoeZPPPFEevPNN9OMGTOyyRmxEmTTTTdNO+64Y64Z481XXMsI1I/Abrvt1mD7q7w1n1cAJK7nXSSvqnIEiisgAFLcvlEzAgQIECBAgAABAgQIECBAgAABAgQIECBAIKeAAEhOOMUIECBAgAABAgQIECBAgAABAgQIECBAgACB4goIgBS3b9SMAAECBAgQIECAAAECBAgQIECAAAECBAgQyCkgAJITTjECBAgQIECAAAECBAgQIECAAAECBAgQIECguAICIMXtGzUjQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEcgoIgOSEU4wAAQIECBAgQIAAAQIECBAgQIAAAQIECBAoroAASHH7Rs0IECBAgAABAgQIECBAgAABAgQIECBAgACBnAICIDnhFCNAgAABAgQIECBAgAABAgQIECBAgAABAgSKKyAAUty+UTMCBAgQIECAAAECBAgQIECAAAECBAgQIEAgp4AASE44xQgQIECAAAECBAgQIECAAAECBAgQIECAAIHiCgiAFLdv1IwAAQIECBAgQIAAAQIECBAgQIAAAQIECBDIKSAAkhNOMQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKC4AgIgxe0bNSNAgAABAgQIECBAgAABAgQIECBAgAABAgRyCgiA5IRTjAABAgQIECBAgAABAgQIECBAgAABAgQIECiugABIcftGzQgQIECAAAECBAgQIECAAAECBAgQIECAAIGcAgIgOeEUI0CAAAECBAgQIECAAAECBAgQIECAAAECBIorIABS3L5RMwIECBAgQIAAAQIECBAgQIAAAQIECBAgQCCngABITjjFCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgeIKCIAUt2/UjAABAgQIECBAgAABAgQIECBAgAABAgQIEMgpIACSE04xAgQIECBAgAABAgQIECBAgAABAgQIECBAoLgCAiDF7Rs1I0CAAAECBAgQIECAAAECBAgQIECAAAECBHIKCIDkhFOMAAECBAgQIECAAAECBAgQIECAAAECBAgQKK6AAEhx+0bNCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgZwCAiA54RQjQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEiisgAFLcvlEzAgQIECBAgAABAgQIECBAgAABAgQIECBAIKeAAEhOOMUIECBAgAABAgQIECBAgAABAgQIECBAgACB4goIgBS3b9SMAAECBAgQIECAAAECBAgQIECAAAECBAgQyCkgAJITTjECBAgQIECAAAECBAgQIECAAAECBAgQIECguAICIMXtGzUjQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEcgoIgOSEU4wAAQIECBAgQIAAAQIECBAgQIAAAQIECBAoroAASHH7Rs0IECBAgAABAgQIECBAgAABAgQIECBAgACBnAICIDnhFCNAgAABAgQIECBAgAABAgQIECBAgAABAgSKKyAAUty+UTMCBAgQIECAAAECBAgQIECAAAECBAgQIEAgp4AASE44xQgQIECAAAECBAgQIECAAAECBAgQIECAAIHiCgiAFLdv1IwAAQIECBAgQIAAAQIECBAgQIAAAQIECBDIKSAAkhNOMQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKC4AgIgxe0bNSNAgAABAgQIECBAgAABAgQIECBAgAABAgRyCgiA5IRTjAABAgQIECBAgAABAgQIECBAgAABAgQIECiugABIcftGzQgQIECAAAECBAgQIECAAAECBAgQIECAAIGcAgIgOeEUI0CAAAECBAgQIECAAAECBAgQIECAAAECBIorIABS3L5RMwIECBAgQIAAAQIECBAgQIAAAQIECBAgQCCngABITjjFCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgeIKCIAUt2/UjAABAgQIECBAgAABAgQIECBAgAABAgQIEMgpIACSE04xAgQIECBAgAABAgQIECBAgAABAgQIECBAoLgCAiDF7Rs1I0CAAAECBAgQIECAAAECBAgQIECAAAECBHIKCIDkhFOMAAECBAgQIECAAAHatnd1AAADbUlEQVQCBAgQIECAAAECBAgQKK6AAEhx+0bNCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgZwCAiA54RQjQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEiisgAFLcvlEzAgQIECBAgAABAgQIECBAgAABAgQIECBAIKeAAEhOOMUIECBAgAABAgQIECBAgAABAgQIECBAgACB4goIgBS3b9SMAAECBAgQIECAAAECBAgQIECAAAECBAgQyCkgAJITTjECBAgQIECAAAECBAgQIECAAAECBAgQIECguAICIMXtGzUjQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEcgoIgOSEU4wAAQIECBAgQIAAAQIECBAgQIAAAQIECBAoroAASHH7Rs0IECBAgAABAgQIECBAgAABAgQIECBAgACBnAICIDnhFCNAgAABAgQIECBAgAABAgQIECBAgAABAgSKKyAAUty+UTMCBAgQIECAAAECBAgQIECAAAECBAgQIEAgp4AASE44xQgQIECAAAECBAgQIECAAAECBAgQIECAAIHiCgiAFLdv1IwAAQIECBAgQIAAAQIECBAgQIAAAQIECBDIKSAAkhNOMQIECBAgQIAAAQIECBAgQIAAAQIECBAgQKC4AgIgxe0bNSNAgAABAgQIECBAgAABAgQIECBAgAABAgRyCgiA5IRTjAABAgQIECBAgAABAgQIECBAgAABAgQIECiugABIcftGzQgQIECAAAECBAgQIECAAAECBAgQIECAAIGcAgIgOeEUI0CAAAECBAgQIECAAAECBAgQIECAAAECBIorIABS3L5RMwIECBAgQIAAAQIECBAgQIAAAQIECBAgQCCngABITjjFCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgeIKCIAUt2/UjAABAgQIECBAgAABAgQIECBAgAABAgQIEMgpIACSE04xAgQIECBAgAABAgQIECBAgAABAgQIECBAoLgCAiDF7Rs1I0CAAAECBAgQIECAAAECBAgQIECAAAECBHIKCIDkhFOMAAECBAgQIECAAAECBAgQIECAAAECBAgQKK6AAEhx+0bNCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgZwCAiA54RQjQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEiivw/wEETEw+4l/W+wAAAABJRU5ErkJggg==" width="640">
</div>

</div>

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Original inputs: Mean=5.1, Low=2.5, High=11.5
New outputs: Mean=5.756166926743772, Low=1.7476288116699656, High=10.824649063148705
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Example-of-the-results-output-table-from-the-find_beta()-method">Example of the results output table from the find_beta() method<a class="anchor-link" href="#Example-of-the-results-output-table-from-the-find_beta()-method">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">e2i</span><span class="o">.</span><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[5]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Test Results</th>
      <th>Mode Value</th>
      <th>Low Value</th>
      <th>High Value</th>
      <th>mean_err</th>
      <th>expected mu</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1839</th>
      <td>1.256205</td>
      <td>2.730769</td>
      <td>0.653846</td>
      <td>23.000000</td>
      <td>0.525004</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>3277</th>
      <td>1.414493</td>
      <td>2.961538</td>
      <td>0.130769</td>
      <td>22.082051</td>
      <td>0.537978</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>278</th>
      <td>1.416464</td>
      <td>2.500000</td>
      <td>0.784615</td>
      <td>22.541026</td>
      <td>0.439332</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>1877</th>
      <td>1.446421</td>
      <td>2.730769</td>
      <td>0.784615</td>
      <td>22.082051</td>
      <td>0.372318</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>3395</th>
      <td>1.451183</td>
      <td>2.961538</td>
      <td>0.523077</td>
      <td>21.164103</td>
      <td>0.385863</td>
      <td>5.1</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="The-df_dist-class-objects-also-have-a-number-of-other-useful-attributes">The df_dist class objects also have a number of other useful attributes<a class="anchor-link" href="#The-df_dist-class-objects-also-have-a-number-of-other-useful-attributes">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">e2i</span><span class="o">.</span><span class="n">name</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[6]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&#39;Incubation Period&#39;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">freq_cont</span><span class="o">.</span><span class="n">checkParams</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Pert vars: mu: 2.6153846153846154, low: 0.0, high: 11.794871794871796
Original inputs: Mean=4, Low=0, High=6
New outputs: Mean=3.715008006792597, Low=1.1877946068174121, High=6.629149733078502
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">cfr</span><span class="o">.</span><span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[8]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Test Results</th>
      <th>Mode Value</th>
      <th>Low Value</th>
      <th>High Value</th>
      <th>mean_err</th>
      <th>expected mu</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11238</th>
      <td>0.000660</td>
      <td>0.007436</td>
      <td>0.000000</td>
      <td>0.058846</td>
      <td>0.000227</td>
      <td>0.015</td>
    </tr>
    <tr>
      <th>11319</th>
      <td>0.001313</td>
      <td>0.007436</td>
      <td>0.000769</td>
      <td>0.060000</td>
      <td>0.000354</td>
      <td>0.015</td>
    </tr>
    <tr>
      <th>12879</th>
      <td>0.001586</td>
      <td>0.008141</td>
      <td>0.000385</td>
      <td>0.060000</td>
      <td>0.000312</td>
      <td>0.015</td>
    </tr>
    <tr>
      <th>12839</th>
      <td>0.001671</td>
      <td>0.008141</td>
      <td>0.000000</td>
      <td>0.060000</td>
      <td>0.000713</td>
      <td>0.015</td>
    </tr>
    <tr>
      <th>16034</th>
      <td>0.001717</td>
      <td>0.009551</td>
      <td>0.000000</td>
      <td>0.054231</td>
      <td>0.000646</td>
      <td>0.015</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>
