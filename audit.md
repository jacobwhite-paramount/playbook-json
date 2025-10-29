# Design System Audit - playbook.json

## Executive Summary
This audit identifies gaps, inconsistencies, and opportunities for unification across the CBS Sports design system tokens. The playbook.json file contains tokens for 12 different brand/platform combinations, with varying levels of completeness and structural differences.

---

## 1. Structural Inconsistencies

### 1.1 Theme/Mode Naming
**Issue:** Inconsistent naming conventions for theme variants across brands.

- **`light`/`dark`**: Used by `247SportsWeb`, `fantasyWeb`, `sportsApp`, `newsWebBison`, `sportsWebBison`, `newsWebFly`, `sportsWebFly`, `newsApp`
- **`default`/`solid`**: Used by `cBSDigitalCTV`
- **`default` only**: Used by `entertainmentWeb` (missing dark variant)
- **`tokens.light`/`tokens.dark`/`tokens.dynamic`**: Used by `fantasyApp` (extra wrapper)

**Recommendation:**
- Standardize on `light` and `dark` naming convention
- Remove `tokens` wrapper from `fantasyApp` to match other brands
- Add `dark` variant to `entertainmentWeb`
- Consider migrating `cBSDigitalCTV` from `default`/`solid` to `light`/`dark` if semantically equivalent

### 1.2 Additional Theme Sections
**Issue:** Some brands have extra theme variants while others don't.

- **`dynamic` variants**: Present in `fantasyApp`, `fantasyWeb`, `sportsApp`, `newsWebBison`, `sportsWebBison`, `newsWebFly`, `sportsWebFly`, `newsApp` (8 brands)
- **`brand` variants**: Present only in `fantasyWeb`, `sportsLineWeb`, `sportsWebFly` (3 brands)
- **Missing in**: `247SportsWeb`, `cBSDigitalCTV`, `entertainmentWeb`

**Recommendation:**
- Document when/why `dynamic` and `brand` themes are used
- Consider adding to all brands for consistency, OR
- Clearly document which brands support which theme variants and why

---

## 2. Property Naming Inconsistencies

### 2.1 Button Property Naming
**Issue:** Three different naming patterns exist for buttons.

**Pattern A** (most common): `buttonPrimaryBackground`, `buttonPrimaryText`, `buttonPrimaryBorder`
- Used by: `247SportsWeb`, `fantasyWeb`, `fantasyApp`, `sportsApp`, `newsWebBison`, `sportsWebBison`, `newsWebFly`, `sportsWebFly`, `newsApp`

**Pattern B**: `buttonBackground`, `buttonText`
- Used by: `cBSDigitalCTV`

**Pattern C**: `buttonPrimaryText` (without Background/Border)
- Used by: `entertainmentWeb`

**Recommendation:**
- Standardize on Pattern A (`buttonPrimaryBackground`, `buttonPrimaryText`, `buttonPrimaryBorder`) as it's most explicit and used by majority
- Migrate `cBSDigitalCTV` to Pattern A
- Complete `entertainmentWeb` with missing Background/Border properties

### 2.2 Text Link Naming
**Issue:** Inconsistent property names for text links.

- **`textLinkPrimary`**: `247SportsWeb`, `fantasyWeb`, `fantasyApp`, `sportsApp`, `newsWebBison`, `sportsWebBison`, `newsWebFly`
- **`textLink`**: `cBSDigitalCTV`, `newsApp`
- **`textLinkPrimary` + `textLinkSecondary`**: `entertainmentWeb`, `fantasyWeb`
- **Missing entirely**: Some brands don't have link states

**Recommendation:**
- Standardize on `textLinkPrimary` with optional `textLinkSecondary` for variants
- Add `textLinkPrimary` to `cBSDigitalCTV` and `newsApp` (can alias `textLink` if they're equivalent)
- Add hover states consistently: `textLinkPrimaryHover`

### 2.3 Surface/Background Naming
**Issue:** Different patterns for surface properties.

- **`surfacePrimary`/`surfaceSecondary`/`surfaceTertiary`**: Most brands
- **`surfaceBackground`**: `cBSDigitalCTV`
- **`surfaceUnselected`/`surfaceSelected`**: `cBSDigitalCTV`
- **Missing hierarchy**: Some brands only have `surfacePrimary`, others have up to tertiary

**Recommendation:**
- Standardize on `surfacePrimary`/`surfaceSecondary`/`surfaceTertiary` naming
- Consider if `surfaceUnselected`/`surfaceSelected` in `cBSDigitalCTV` should be renamed to match pattern or if they represent different concepts

### 2.4 Overlay Naming Chaos
**Issue:** Multiple naming patterns for overlay properties.

- **`surfaceOverlaySolid`**: `newsApp`
- **`surfaceOverlayTopGradient`**: `newsApp`
- **`surfaceOverlayBottomGradient`**: `newsApp`
- **`surfaceOverlayLinearFull`**: `newsWebBison`, `sportsWebBison`, `newsWebFly`, `sportsWebFly`
- **`surfaceOverlayLinearHalf`**: `newsWebBison`, `sportsWebBison`, `newsWebFly`, `sportsWebFly`
- **`overlaysSolid`**: `entertainmentWeb`
- **`overlayLinearPrimary`**: `entertainmentWeb`
- **`overlayLinearSecondary`**: `entertainmentWeb`
- **`cardOverlayBottom`**: `cBSDigitalCTV`
- **`cardOverlayBrand`**: `cBSDigitalCTV`

**Recommendation:**
- **CRITICAL**: Unify overlay naming across all brands
- Suggested standard: `surfaceOverlaySolid`, `surfaceOverlayTop`, `surfaceOverlayBottom`, `surfaceOverlayFull`
- Map gradients with clear naming: `surfaceOverlayFullGradient`, `surfaceOverlayHalfGradient`, `surfaceOverlayTopGradient`, `surfaceOverlayBottomGradient`

---

## 3. Missing Properties & Gaps

### 3.1 Button States - Incomplete Coverage

#### Missing Hover States
- **`cBSDigitalCTV`**: Missing ALL hover states (`buttonBackgroundHover`, `buttonTextHover`, etc.)
- **`entertainmentWeb`**: Has `buttonPrimaryTextHover` but missing `buttonPrimaryBackgroundHover`
- **`fantasyApp`**: Missing hover states for most button variants
- **`newsApp`**: Missing hover states for most button variants

**Recommendation:**
- Audit each brand and ensure Primary, Secondary, and Tertiary buttons all have hover states
- Standard set: `BackgroundHover`, `TextHover`, `BorderHover`

#### Missing Focus States
- **Present**: `fantasyWeb`, `newsWebFly`, `sportsWebFly` (have `BorderFocused` variants)
- **Missing**: All other brands

**Recommendation:**
- Add focus states to all brands for accessibility compliance
- Standard: `buttonPrimaryBorderFocused`, `buttonSecondaryBorderFocused`, `buttonTertiaryBorderFocused`

#### Missing Disabled States
- **Complete**: Most brands have disabled states
- **Incomplete**: Some brands missing `buttonDisabledBorder` or using inconsistent naming
- **Missing**: `cBSDigitalCTV` has no disabled variant

**Recommendation:**
- Ensure each brand has complete disabled state: `buttonDisabledBackground`, `buttonDisabledBorder`, `buttonDisabledText`

#### Missing Loading States
- **Present**: `247SportsWeb`, `sportsApp`, `newsApp`, `fantasyWeb`, `sportsLineWeb` (some variants)
- **Missing**: `cBSDigitalCTV`, `entertainmentWeb`, `fantasyApp`

**Recommendation:**
- Add loading states where applicable: `buttonLoadingBackground`, `buttonLoadingBorder`, `buttonLoadingIconActive`, `buttonLoadingIconInactive`

### 3.2 Button Variants - Missing Types

#### Destructive Buttons
- **Present**: `sportsApp`, `newsApp` (have `buttonDestructivePrimary`, `buttonDestructiveSecondary`, `buttonDestructiveTertiary`)
- **Missing**: All other brands

**Recommendation:**
- Add destructive button variants to all brands that need error/delete actions
- Standard: `buttonDestructivePrimaryBackground`, `buttonDestructivePrimaryText`, `buttonDestructiveSecondary*`, `buttonDestructiveTertiaryText`

#### Toggle Buttons
- **Present**: `sportsApp`, `fantasyWeb`, `newsApp`, `sportsLineWeb` (some variants)
- **Inconsistent naming**: 
  - `buttonToggleUnselected*` / `buttonToggleSelected*` (most)
  - `buttonToggleButtonUnselected*` / `buttonToggleButtonSelected*` (`newsWebFly`, `sportsWebFly`)
- **Missing**: `247SportsWeb`, `cBSDigitalCTV`, `entertainmentWeb`, `fantasyApp`

**Recommendation:**
- Standardize on `buttonToggleUnselected*` / `buttonToggleSelected*` (remove extra "Button" word)
- Add toggle buttons to brands that need them

#### Promo/Live Buttons
- **Present**: `fantasyWeb`, `sportsWebBison`, `newsWebFly`, `sportsWebFly` (have promo/live variants)
- **Missing**: Other brands

**Recommendation:**
- Document which brands need promotional/special action buttons
- Standardize naming: `buttonPromoPrimary*`, `buttonLive*`

#### Odds Buttons (SportsLineWeb specific)
- **Present**: Only `sportsWebBison`, `sportsWebFly` have `buttonOdds*` variants
- **Note**: This is brand-specific, which is appropriate

### 3.3 Text Properties - Missing Variants

#### Status Text Colors
- **Complete**: Most brands have `textPositive`, `textNegative`, `textAlert`
- **Missing/Wrong**: 
  - `cBSDigitalCTV` only has `textAlert` (missing positive/negative)
  - `entertainmentWeb` missing status text variants
  - Some brands have `textWarning`, `textInformation`, `textHot`, `textWarm`, `textCool` while others don't

**Recommendation:**
- Standardize core status colors: `textPositive`, `textNegative`, `textWarning`, `textAlert`
- Document which brands need extended status colors (Hot/Warm/Cool)

#### Link States
- **Incomplete**: Many brands missing hover/disabled states for links
- **Missing**: `textLinkDisabled` (only `entertainmentWeb` has it)

**Recommendation:**
- Add `textLinkPrimaryHover` and `textLinkDisabled` to all brands

### 3.4 Table Properties - Inconsistent Structure

**Issue:** Table properties vary significantly across brands.

**Patterns observed:**
- **Full table properties**: `247SportsWeb`, `fantasyWeb`, `sportsWebBison`, `newsWebBison` (have comprehensive table tokens)
- **Minimal/Inconsistent**: Other brands have partial table properties
- **Naming inconsistencies**:
  - `tableBaseBackground` vs `tableBase*`
  - `tableHeaderRowBackground` vs `tableHeaderColumnBackground*`
  - `tableBodyRowBackground*` vs `tableBodyColumnBackground*`

**Recommendation:**
- Standardize table property structure across all brands
- Core set: `tableBaseBackground`, `tableBaseBorderPrimary`, `tableBaseBorderSecondary`
- Header: `tableHeaderRowBackground`, `tableHeaderText`, `tableHeaderTextHover`, `tableHeaderColumnBackgroundPrimary`, `tableHeaderColumnBackgroundSecondary`
- Body: `tableBodyRowBackgroundPrimary`, `tableBodyRowBackgroundSecondary`, `tableBodyRowBackgroundHover`, `tableBodyTextPrimary`, `tableBodyTextSecondary`, `tableBodyColumnBackgroundActive`

### 3.5 Elevation/Shadow System

**Issue:** Elevation properties are inconsistently implemented.

**Current state:**
- **Basic `elevation`**: Present in most brands (single value)
- **Extended system**: Some brands have `elevationRaised`, `elevationNavigation`, `elevationModal` (`fantasyWeb`, `newsApp`, `sportsApp`)
- **Numbered system**: `newsWebFly`, `sportsWebFly` have `elevation0`, `elevation5`, `elevation10`, `elevation20`, `elevation30`, `elevation40`, `elevation50`
- **Partial**: `cBSDigitalCTV` only has `elevation5` and `elevation20`
- **Missing**: `247SportsWeb`, `entertainmentWeb`, `fantasyApp` have no elevation properties

**Recommendation:**
- Standardize on numbered elevation system: `elevation0` through `elevation50` (or similar scale)
- OR use semantic names: `elevationRaised`, `elevationNavigation`, `elevationModal`
- Decide on one approach and apply consistently
- Add elevation properties to all brands

### 3.6 Gradient Properties

**Issue:** Gradient implementations vary and naming is inconsistent.

**Current state:**
- **Gradients present**: Most brands have some gradient properties
- **Naming inconsistency**: Same gradients named differently (`surfaceOverlayLinearFull` vs `overlayLinearPrimary`)
- **Missing**: Some brands missing gradient overlays entirely

**Recommendation:**
- Standardize gradient naming across all brands
- Ensure overlay gradients are available in all brands that need them
- Consider if sport-specific gradients (like fantasyApp's sport/position gradients) should be in a shared location

---

## 4. Brand-Specific Issues

### 4.1 cBSDigitalCTV
- **Minimal button system**: Only has `buttonBackground`, `buttonBackgroundSelected`, `buttonText`, `buttonTextSelected`
- **Missing**: Hover, focus, disabled, loading states
- **Different naming**: Uses `surfaceBackground` instead of `surfacePrimary`
- **Has unique properties**: `utilityBorderSecondary`, `utilityBorderSelected` (gradients), `cardOverlayBottom`, `cardOverlayBrand`

**Recommendation:**
- Expand button system to match standard pattern
- Add missing states (hover, focus, disabled)
- Consider if unique properties are truly brand-specific or should be standardized

### 4.2 entertainmentWeb
- **Only has `default` theme**: Missing dark variant
- **Incomplete button properties**: Missing Background/Border for primary buttons
- **Unique overlay naming**: Uses `overlaysSolid`, `overlayLinearPrimary`, `overlayLinearSecondary`

**Recommendation:**
- Add dark theme variant
- Complete button property set
- Align overlay naming with standard

### 4.3 fantasyApp
- **Extra `tokens` wrapper**: Unnecessary nesting that differs from other brands
- **Missing button states**: No hover, focus states
- **Has unique properties**: Sport/position gradients, playoff gradients (appropriate for fantasy)

**Recommendation:**
- Remove `tokens` wrapper to match other brands
- Add missing button states where applicable
- Keep brand-specific fantasy properties (they're domain-appropriate)

### 4.4 sportsLineWeb
- **Brand-specific properties**: `gradientWin`, `gradientLoss`, `gradientNeutral`, `gradientPush` (appropriate for betting/sportsline)

**Recommendation:**
- Keep brand-specific properties
- Ensure core properties follow standard naming

---

## 5. Unification Opportunities

### 5.1 Shared Color Palette
**Opportunity:** Many brands share similar color values that could be extracted.

**Common patterns observed:**
- **Primary blue**: `#004ace` appears in multiple brands
- **247Sports blue**: `#00249e` appears in multiple brands
- **Status colors**: Green (`#037f2d`, `#059646`), Red (`#cc0d00`, `#e10400`), Yellow (`#eaaa17`) are very similar
- **Neutral grays**: Many shared values like `#181818`, `#5f5f5f`, `#767676`, `#ababab`, `#dcdcdc`, `#e8e8e8`, `#f2f2f2`

**Recommendation:**
- Create a base color palette that can be referenced
- Use semantic color tokens that brands can override
- Document when brand-specific colors are intentional vs. when they could use shared values

### 5.2 Standard Button System
**Opportunity:** Create a base button system that all brands extend.

**Core button variants needed:**
1. Primary (with Background, Border, Text, Hover, Focus, Disabled, Loading)
2. Secondary (same states)
3. Tertiary (same states)
4. Destructive (Primary/Secondary/Tertiary variants)
5. Toggle (Unselected/Selected with all states)
6. Loading (Background, Border, Icon states)

**Recommendation:**
- Define a "base" button system in documentation
- Ensure all brands that need buttons have this complete set
- Use consistent naming across all brands

### 5.3 Common Utility Properties
**Opportunity:** Standardize utility/tooling properties.

**Common utilities:**
- `utilityBorder`, `utilityDisabled`
- `utilityIconPrimary`, `utilityIconSecondary`
- `utilityStatusPositive`, `utilityStatusNegative`, `utilityStatusWarning`, `utilityStatusAlert`
- `utilityUIElementActive`, `utilityUIBackground`, `utilityUIBackgroundHover`

**Recommendation:**
- Ensure all brands have a consistent utility property set
- Document which utilities are brand-specific extensions vs. standard

---

## 6. Data Quality Issues

### 6.1 Color Format Consistency
- Most colors use hex format (`#ffffff`)
- Some use hex with alpha (`#ffffff00`, `#00000066`)
- Some gradients embed hex values within gradient strings

**Recommendation:**
- Ensure all hex colors are consistently formatted
- Document alpha channel usage patterns

### 6.2 Missing vs. Null Values
- Some properties might be intentionally absent vs. missing
- Empty strings vs. missing keys unclear

**Recommendation:**
- Document intentional omissions
- Consider using consistent "placeholder" values if intentional

### 6.3 Typo/Inconsistency Notes
- `brandSportsline` vs `brandSportsLine` (capitalization inconsistency)
- `brandMaxpreps` vs `brandMaxPreps` (capitalization)
- `brandCBSSports` vs `brand247Sports` vs `brandSportsline` (naming pattern inconsistency)

**Recommendation:**
- Standardize brand name capitalization and naming patterns

---

## 7. Recommended Action Items

### High Priority
1. ✅ **Standardize theme naming**: Migrate all to `light`/`dark`
2. ✅ **Unify overlay property naming**: Critical for consistency
3. ✅ **Complete button state coverage**: Add hover/focus/disabled/loading where missing
4. ✅ **Standardize button property naming**: Use `buttonPrimaryBackground` pattern everywhere
5. ✅ **Add elevation system**: Standardize and add to all brands

### Medium Priority
6. ⚠️ **Add dark theme to entertainmentWeb**
7. ⚠️ **Remove `tokens` wrapper from fantasyApp**
8. ⚠️ **Standardize table properties** across all brands
9. ⚠️ **Add focus states** for accessibility
10. ⚠️ **Standardize text link naming** and add missing states

### Low Priority
11. 📝 **Document brand-specific extensions**: Fantasy gradients, SportsLine odds buttons
12. 📝 **Create base color palette**: Extract common colors
13. 📝 **Fix capitalization inconsistencies**: Brand name properties
14. 📝 **Document missing properties**: When intentional vs. oversight

---

## 8. Potential Architecture Improvements

### 8.1 Hierarchical Token System
**Current:** Flat structure with brand → theme → properties

**Potential improvement:**
- Base tokens → Brand overrides → Theme variants
- Shared tokens file that brands extend
- Semantic tokens that reference base palette

### 8.2 Property Groups
**Suggestion:** Organize properties into logical groups:
- `button.*`
- `text.*`
- `surface.*`
- `utility.*`
- `table.*`
- `brand.*`

(Note: This would be a structural change, but could improve discoverability)

### 8.3 Documentation Standard
**Suggestion:** Add inline documentation or companion docs that describe:
- When to use each property
- Relationships between properties
- Brand-specific guidance
- Accessibility considerations

---

## Summary Statistics
- **Total brands**: 12
- **Themes per brand**: 1-4 (most have 2-3)
- **Total unique properties**: ~200+ (varies by brand)
- **Common property coverage**: ~60-70% across brands
- **Critical gaps**: Button states, Focus states, Elevation system, Overlay naming

