# Non-Breaking Versioning (NonBreakVer)

![Example with a version number: 1.6.4, this translates to Milestone: 1, Minor: 6, Patch: 4](./assets/NonBreakVer_example.png)

## Format **`X.Y.Z`**

1. **`MILESTONE (X.0.0)`:** Incremented for **major milestones**, system-wide architectural rewrites, scope expansions, or significant evolution of the project.
2. **`MINOR (0.Y.0)`:** Incremented for **new backward-compatible features**, new functionality, content, or non-disruptive enhancements.
3. **`PATCH (0.0.Z)`:** Incremented for **fixes or corrections**, documentation updates, and maintenance.

## NonBreakVer

An intuitive versioning specification for non-breaking software, design systems, and content-first projects where traditional breaking changes do not apply.

## Introduction

Rather than introducing a novelty for its own sake, this is simply the formalization of an existing practice that - to the best of my knowledge - doesn't seem to have a standardized reference or a formal specification.

Most people perceive a new major version of anything, a product, an app or a game, that you can expect some big changes, new content or design, but that's not how the **[Semantic Versioning](https://semver.org/)** standard works - because that's not what it was trying to communicate or solve.

### Semantic Versioning

For **Semantic Versioning**, it's only a new major version when there are breaking changes. So it can be a design overhaul, a complete rewrite of a code base or a lot of new improvements and features and it will still be considered a **minor change** if no compatibility was broken in the updated version.

This concept doesn't communicate well when there is a new milestone, be it for marketing reasons or for our own understanding of something that deserves more attention. And this restriction is the main reason a lot of people and companies chose to introduce their own way of versioning.

The downside of this is that either the user has try to understand it by context or you have to make a bit more explicit how your own versioning works - without being able to simply reference the spec you follow.

### Other Versioning Specs

**[Romantic Versioning](https://github.com/romversioning/romver)** and **[Pragmatic Versioning](https://github.com/pragver/pragver)** also try to address this confusion. Despite the different naming convention - **`PROJECT`** for **RomVer** and **`GRADE`** for **PragVer** -, the bottom line is that a new major version means that the project or product has achieved a new milestone.

#### Romantic Versioning

**RomVer** tries to focus more on the user - that usually doesn't care or understand what is considered **`MINOR`** or **`PATCH`** -, so it combines both into a single number at the end. It follows this format **1.0.0 (`PROJECT.MAJOR.MINOR/PATCH`):**

- **`MAJOR`:** Breaking changes
- **`MINOR/PATCH`**: Non-breaking changes

Which might be good for the user but you lose the granularity of easily understanding if the new version has new features or just some fixes and corrections.

#### Pragmatic Versioning

**PragVer** tackles it in a different way, it basically adds **`GRADE`** in front of Semantic Versioning so it's easy to understand when there is a new disruptive version, it has 4 numbers following the **1.0.0.0 (`GRADE.MAJOR.MINOR.PATCH`)** format.

This solves the confusion and it keeps the convention that **SemVer** already established. But now there is an extra number and for things that don't have breaking changes, they would have a carry an unnecessary **`0`** in the middle of the version.

## The Solution

**NonBreakVer** exchanges **`MAJOR`** in favor of **`MILESTONE`**, while retaining standard **SemVer** mechanics for the lower digits **`MINOR`** and **`PATCH`**.

## Guiding Principles

- **Zero-Rupture Guarantee:** Updating a **NonBreakVer** project must never break user configurations, editor/environment compatibility, or any previously working setup — regardless of which segment of the version number changes.
- **Additive Mechanics:** Features and properties are added, refined, or sanitized. Deprecations must be handled gracefully without dropping support abruptly.
- **Intuitive Versioning:** The **`MILESTONE`** number communicates a version progression that people intuitively understand, while **`MINOR`** and **`PATCH`** maintain precision for tooling and tracking at a glance.

## Non-Breaking Versioning Specification

**1.** Version numbers take the form **`MILESTONE.MINOR.PATCH[-PRE][+BUILD]`**, where **`MILESTONE`**, **`MINOR`**, and **`PATCH`** are non-negative integers with no leading zeroes, and **`PRE`** and **`BUILD`** are optional identifiers made up of ASCII alphanumerics, hyphens, and dots.

**2.** This scheme is meant for projects that, by nature, never have a public API to break — visual themes, fonts, palettes, datasets, or specs, for example. If your project _can_ break compatibility, this isn't the right scheme for it.

**3.** Once a release is out, its contents shouldn't change. If something needs fixing, ship it as a new release instead.

**4.** **`MILESTONE`** version zero (**`0.x.x`**) is for initial development, before the project is considered stable.

**5.** Each release's version number builds on the one before it, following the next two rules.

**6.** Bump **`MILESTONE`** when the release feels significant enough to mark a new era for the project — a big enough combination of new content, structural change, or overall impact that it deserves to stand apart from what came before. This is a judgment call by whoever maintains the project, not a fixed rule. When **`MILESTONE`** bumps, **`MINOR`** and **`PATCH`** reset to **`0`**.

**7.** Otherwise, bump **`MINOR`** when the release adds anything new — content, functionality, capability — in a way that doesn't take anything away from what already existed. When **`MINOR`** bumps, **`PATCH`** resets to **`0`**.

**8.** Otherwise, bump **`PATCH`** — this covers releases that only fix or correct something, without adding anything new.

**9.** A pre-release version can be marked by appending a hyphen and a dot-separated identifier right after **`PATCH`**, made only of alphanumerics, dots, and hyphens. Pre-release identifiers can't be empty, and are only meant for unstable previews of a future release.

Examples: **`1.0.0-alpha`**, **`1.0.0-alpha.1`**, **`1.0.0-0.3.7`**.

**10.** Build metadata can be added by appending a plus sign and a dot-separated identifier right after the pre-release identifier (or **`PATCH`**, if there's no pre-release tag). Same character rules apply, and it's only for identifying a specific build of a release, not the release itself.

Examples: **`1.0.0-alpha+001`**, **`1.0.0+20260918`**, **`1.0.0-beta+exp.sha.5114f85`**.

**11.** To compare versions, check **`MILESTONE`** first — if they differ, that decides it. If not, check **`MINOR`**, then **`PATCH`**. If all three match, a pre-release version always ranks lower than the equivalent normal release.

Example: **`1.0.0 < 2.0.0 < 2.1.0 < 2.1.1 < 2.1.2-rc.1 < 2.1.2-rc2 < 2.1.2`**.

## Non-Breaking Changes Project Types

- **Editorial/documentation content** — guides, FAQs, published books/chapters, not specs.
- **Visual themes** — color themes, icon themes, UI themes.
- **Wallpapers, icon packs, cursor packs** — same logic as themes.
- **Typefaces / fonts** — adding weights, glyphs, or adjusting kerning never breaks existing installs.
- **Non-programmatic configuration presets** — camera presets, audio EQ presets, color LUTs.
- **Cosmetic game assets** — skins, maps, textures.
- **Résumés, slide decks, presentations** — no technical dependency involved.
- **Informal specs/conventions** — no programmatic consumer to break by reading a new version.

## License

[CC BY 4.0 (Creative Commons — Attribution 4.0 International)](https://creativecommons.org/licenses/by/4.0/)

- Anyone is free to **share** (copy and redistribute in any medium or format) and **adapt** (remix, transform, build upon) the material, for any purpose, including commercial,
- **Attribution**: you must give appropriate credit to the original author, provide a link to the license, and indicate if changes were made.
- No additional restrictions may be applied that would prevent others from doing what the license permits. It's one of the most permissive **Creative Commons** licenses — the only requirement is attribution.

[![Creative Commons — Attribution 4.0 International (CC BY 4.0)](./assets/CC_BY_icon.svg)](https://creativecommons.org/licenses/by/4.0/)
