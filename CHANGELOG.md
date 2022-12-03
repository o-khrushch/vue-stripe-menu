# Changelog

All notable changes to this project will be documented in this file. See [standard-version](https://github.com/conventional-changelog/standard-version) for commit guidelines.

### [3.0.0-beta.1](https://github.com/oleksiikhr/vue-stripe-menu/compare/v2.1.1...3.0.0-beta.1) (2021-08-08)

- Replacing the style calculation for background (https://github.com/oleksiikhr/vue-stripe-menu/issues/246).

**before**

```scss
.vsm-background {
  transform: translate(152px, 0px) scaleX(1.08421) scaleY(1.2125);
}
```

**after**

```scss
.vsm-background {
  transform: translate(246px, 10px);
  width: 409px;
  height: 485px;
}
```

- Build files

**before**

```
dist/demo.html
dist/vue-stripe-menu.common.js
dist/vue-stripe-menu.common.js.map
dist/vue-stripe-menu.css
dist/vue-stripe-menu.umd.js
dist/vue-stripe-menu.umd.js.map
dist/vue-stripe-menu.umd.min.js
dist/vue-stripe-menu.umd.min.js.map
```

**after**

```
dist/vue-stripe-menu.css
dist/vue-stripe-menu.es.js
dist/vue-stripe-menu.umd.js
```

---

- [TypeScript](https://www.typescriptlang.org/) added.
- Improved [ESLint](https://eslint.org/) configs, added [Prettier](https://prettier.io/) and [Stylelint](https://stylelint.io/).
- Added Github documents: code of conduct, contributors and issue templates.
- Installed [Node.js](https://nodejs.org/) as core `16.15.0`.
- Replaced [yarn](https://yarnpkg.com/) with [pnpm](https://pnpm.io/).
- Replaced [CircleCI](https://circleci.com/) with [Github Actions](https://github.com/features/actions).
- Removed build documentation files from the repository. The current build is in the [gh-pages](https://github.com/oleksiikhr/vue-stripe-menu/tree/gh-pages) branch.
- Added more workflows:
  - Additional code check using [CodeQL](https://codeql.github.com/).
  - Automatic publishing to [npm](https://www.npmjs.com/) from main branch.

### [2.1.1](https://github.com/oleksiikhr/vue-stripe-menu/compare/v2.1.0...v2.1.1) (2021-08-08)

* Migrate from deprecated libSass (node-sass library) to Dart Sass ([944ad5d3](https://github.com/oleksiikhr/vue-stripe-menu/commit/944ad5d33fbd648a5c3a5b5a5833e283b3bdd0f1))

## [2.1.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v2.0.0...v2.1.0) (2021-06-27)


### Features

* **menu:** add align props ([1991c9f](https://github.com/oleksiikhr/vue-stripe-menu/commit/1991c9f13d807441695149e251ef8b587c71f6ce))


### Bug Fixes

* **mobile:** emit v-model props on vue-3 ([a791be8](https://github.com/oleksiikhr/vue-stripe-menu/commit/a791be829cb4445242d7f7af22dbd81633e2a6c3))

## [2.0.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.5.0...v2.0.0) (2021-04-09)

### Global changes

> To reduce the number of override styles, unnecessary classes and so on, many styles/classes have been added/changed or removed!

- Added the ability to customize styles in realtime via [Demo Website](https://oleksiikhr.github.io/vue-stripe-menu/)
- Added a simplified demo of the component to the [#Install section](https://oleksiikhr.github.io/vue-stripe-menu/#install)
- Replace default bundle from **vue-stripe-menu.common.js** to **vue-stripe-menu.umd.min.js**
- Fixed animation with problematic dropdown-transition (see new `transition-timeout` props)
- Now, when the screen width changes `window.addEventListener('resize')`, the following happens:
    - dropdown is open - location is being recalculated (`resizeDropdown` function)
    - dropdown is closed - improved logic of instant destruction of styles
- Added the ability not to install the component globally:

```vue
import { VsmMenu, VsmMob } from 'vue-stripe-menu'

export default {
  components: {
    VsmMenu, VsmMob
  }
}
```

- Add styles:

```scss
// These default values have been removed from the library (default font-size is yours)
.vsm-link, .vsm-mob-content__wrap {
  font-size: 17px;
  font-weight: 500;
}

.vsm-root > li {
  // display: flex; // <-- default display removed
  // All override classes from .vsm-section
}

// Change 768px on your value from $vsm-media, if set
@media screen and (max-width: 768px) {
  .vsm-mob-show {
    display: block;
  }
  .vsm-mob-hide {
    display: none;
  }
  .vsm-mob-full {
    flex-grow: 1;
  }
}
```

- Change the code/styles according to the changes below

### Style changes

- Removed `cursor: default` from dropdown buttons with HTML element `<a href="" />`
- Removed `@media` styles
- Removed predefined `font-size: 17px` and `font-weight: 500`
- Renamed [variables](https://github.com/oleksiikhr/vue-stripe-menu/blob/main/src/scss/_variables.scss):
    - `$vsm-menu-border-radius` > `$vsm-border-radius`
    - `$vsm-menu-transform-content` > `$vsm-transform-content`
    - `$vsm-menu-link-height` > `$vsm-link-height`
    - `$vsm-menu-arrow-shadow` > `$vsm-arrow-shadow`
    - `$vsm-mob-size` > `$vsm-mob-hamburger-size`
- Added [variables](https://github.com/oleksiikhr/vue-stripe-menu/blob/main/src/scss/_variables.scss):
    - Menu: `$vsm-arrow-size`, `$vsm-arrow-shadow`, `$vsm-arrow-border-radius`, `$vsm-index`, `$vsm-background`,
      `$vsm-background-alt`, `$vsm-background-arrow`, `$vsm-link-padding`
    - Mob: `$vsm-mob-dropdown-offset`, `$vsm-mob-dropdown-border-radius`, `$vsm-mob-close-weight`, `$vsm-mob-close-color`,
      `$vsm-mob-close-color-hover`, `$vsm-mob-link-offset`, `$vsm-mob-background`, `$vsm-mob-shadow`, `$vsm-mob-transition`,
      `$vsm-mob-transition-link`

### Classes changes

- Removed
    - `vsm-section` (now `list-style: none` set from parent `.vsm-root > li`)
- Renamed
    - `vsm-section_menu` > `vsm-link-container`
    - `vsm-section_mob` > `vsm-mob-container`

### Components

#### Menu

- Attribute added to each link [tabindex="0"](https://github.com/oleksiikhr/vue-stripe-menu/blob/main/src/components/Menu.vue#L26)

**[Props](https://github.com/oleksiikhr/vue-stripe-menu#menu-props)**

These 2 properties have been removed due to unnecessary use, as well as dependence on css styles (width and height are overridden on the first interaction)

- Removed `base-width`
- Removed `base-height`

Added the ability to indent the dropdown menu from links

- Added `dropdown-offset`
- Added `transition-timeout`

**[Methods](https://github.com/oleksiikhr/vue-stripe-menu#menu-methods)**

When changing dynamic content inside dropdown, you can now call `resizeDropdown` via `$refs`, resizing and relocating the dropdown

- Added `resizeDropdown`

**[Properties](https://github.com/oleksiikhr/vue-stripe-menu#menu-properties)**

- Removed `hasDropdownEls`
- Removed `$refs.links`
- Added `itemsWithDropdown`
- Added `elementsWithDropdown`
- Added `dropdownContainerItems`

#### Mob

**[Slots](https://github.com/oleksiikhr/vue-stripe-menu#mob-slots)**

Added the ability to replace the **close button** after opening the dropdown menu

- Added `close`

#### Other

**[Classes](https://github.com/oleksiikhr/vue-stripe-menu#classes)**

- Removed `vsm-mob-full`
- Added `vsm-mob-show`


## [1.5.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.4.0...v1.5.0) (2020-11-17)


### Features

* **mob:** add closeDropdown method ([44afeca](https://github.com/oleksiikhr/vue-stripe-menu/commit/44afeca79f5434d70fc275d161a9102fe1e8a8c7))

## [1.4.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.3.1...v1.4.0) (2020-09-27)


### Features

* delete core-js library from deps ([5a99691](https://github.com/oleksiikhr/vue-stripe-menu/commit/5a9969163bdf5d6e9cec00e51f4472c163fb3c8a))

### [1.3.1](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.3.0...v1.3.1) (2020-09-03)


### Bug Fixes

* hide dropdown after scroll on mobile browser ([af0467c](https://github.com/oleksiikhr/vue-stripe-menu/commit/af0467c6f7a859d11ba9f94834d4dbcf1e6e3ffc))

## [1.3.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.12...v1.3.0) (2020-08-24)


### Features

* new handler props ([a64d090](https://github.com/oleksiikhr/vue-stripe-menu/commit/a64d09003cb8f60affc99e7722af565321cc6ec0))


### Bug Fixes

* **tests:** change _vsm_menu to _vsmMenu ([2ccd5e9](https://github.com/oleksiikhr/vue-stripe-menu/commit/2ccd5e938f407caa4d09c935a68d75dc73aaa666))

### [1.2.12](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.11...v1.2.12) (2020-08-06)

### [1.2.11](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.10...v1.2.11) (2020-05-24)


### Bug Fixes

* **tests:** isolate component for each test, replace deprecated code ([6628213](https://github.com/oleksiikhr/vue-stripe-menu/commit/6628213506da279eb24d79a9b45134ecc2c375a1))

### [1.2.10](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.9...v1.2.10) (2020-04-28)


### Bug Fixes

* font blurring ([384fb78](https://github.com/oleksiikhr/vue-stripe-menu/commit/384fb78e7c78626e0002b86ed18800e35501324b))

### [1.2.9](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.8...v1.2.9) (2020-04-26)


### Bug Fixes

* accept component with dropdown menu ([a0072f4](https://github.com/oleksiikhr/vue-stripe-menu/commit/a0072f4649ea0379b2294e407893a96a24f16ed6))

### [1.2.8](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.7...v1.2.8) (2020-04-07)

### [1.2.7](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.6...v1.2.7) (2020-03-14)

### [1.2.6](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.5...v1.2.6) (2020-02-02)


### Bug Fixes

* rewrite calculate logic for display dropdown menu ([ec99f82](https://github.com/oleksiikhr/vue-stripe-menu/commit/ec99f8224b38708983ebd5f3ab37a9ddefe3f32c))

### [1.2.5](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.4...v1.2.5) (2020-01-30)


### Bug Fixes

* get HTML Element from Vue component ([8e37831](https://github.com/oleksiikhr/vue-stripe-menu/commit/8e378318f3e452fc6868d08eb5ca36a0b20c7f5e))

### [1.2.4](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.3...v1.2.4) (2020-01-13)

### [1.2.3](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.2...v1.2.3) (2019-12-14)

### [1.2.2](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.1...v1.2.2) (2019-11-30)


### Bug Fixes

* accept classes for vsm-link ([78f3d70](https://github.com/oleksiikhr/vue-stripe-menu/commit/78f3d704886c7117a1a01f6a428f5a6f797a6baf))
* correct calculate width ([5f0c17a](https://github.com/oleksiikhr/vue-stripe-menu/commit/5f0c17a00d669191ad6dde5132dac0e661ce956b))
* dropdown height and width calculation ([9e0de75](https://github.com/oleksiikhr/vue-stripe-menu/commit/9e0de755b091a7cbc486aa3f0c67b72447b6abd7))

### [1.2.1](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.2.0...v1.2.1) (2019-10-27)


### Bug Fixes

* horisontal scroll after window resize ([a543312](https://github.com/oleksiikhr/vue-stripe-menu/commit/a543312))
* run on SSR ([415d43c](https://github.com/oleksiikhr/vue-stripe-menu/commit/415d43c))



## [1.2.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.1.0...v1.2.0) (2019-10-26)


### Features

* support override scss styles and add more variables ([dc84d4b](https://github.com/oleksiikhr/vue-stripe-menu/commit/dc84d4b))



## [1.1.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v1.0.0...v1.1.0) (2019-10-26)


### Bug Fixes

* correct display border-radius on cut div ([fd0415f](https://github.com/oleksiikhr/vue-stripe-menu/commit/fd0415f))
* hide dropdown content on hover arrow ([ffa5aa1](https://github.com/oleksiikhr/vue-stripe-menu/commit/ffa5aa1))


### Features

* add scss variables, hamburger ([aea0989](https://github.com/oleksiikhr/vue-stripe-menu/commit/aea0989))
* add vsm-mob component ([1d55028](https://github.com/oleksiikhr/vue-stripe-menu/commit/1d55028))



## [1.0.0](https://github.com/oleksiikhr/vue-stripe-menu/compare/v0.1.0...v1.0.0) (2019-10-19)


### Bug Fixes

* check offset width for cut ([f0716d5](https://github.com/oleksiikhr/vue-stripe-menu/commit/f0716d5))
* correct link in docs ([50a5941](https://github.com/oleksiikhr/vue-stripe-menu/commit/50a5941))
* get window/document on SSR ([1c2be1b](https://github.com/oleksiikhr/vue-stripe-menu/commit/1c2be1b))
* publish dist to npm ([6625f75](https://github.com/oleksiikhr/vue-stripe-menu/commit/6625f75))
* run demo (component import) ([851966f](https://github.com/oleksiikhr/vue-stripe-menu/commit/851966f))


### Features

* prepare for tests (packages, config) ([e215a67](https://github.com/oleksiikhr/vue-stripe-menu/commit/e215a67))
* support mobile (window right offset), new screen-offset props ([4bb113e](https://github.com/oleksiikhr/vue-stripe-menu/commit/4bb113e))
