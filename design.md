Here’s a comprehensive style guide pulled straight from your Toma v2 Beta screenshots. You can feed this into your AI-powered prototyping tool to get an identical look-and-feel.

---

## 1. Color Palette

| Name                   | Hex       | Usage                                         |
| ---------------------- | --------- | --------------------------------------------- |
| **Black**              | `#000000` | Primary nav background, footer, text on black |
| **Rich Charcoal**      | `#1A1A1A` | Sidebar items (hover), headers on dark BG     |
| **Pure White**         | `#FFFFFF` | Page background, cards, text on dark BG       |
| **Cool Gray (100)**    | `#F5F5F5` | Card backgrounds (light), input fields        |
| **Warm Gray (300)**    | `#D1D5DB` | Borders, dividers                             |
| **Neutral Gray (500)** | `#6B7280` | Secondary text, placeholder text              |
| **Text Gray (900)**    | `#111827` | Primary body text, headings on white BG       |
| **Accent Blue**        | `#38B6FF` | Primary buttons, links, selected states       |
| **Accent Deep Blue**   | `#005F96` | Hover / active states on primary buttons      |
| **Success Green**      | `#22C55E` | Positive stats, success badges                |
| **Warning Yellow**     | `#FBBF24` | Warning badges (e.g. Low inventory)           |
| **Error Red**          | `#EF4444` | Negative stats, error badges                  |

---

## 2. Typography

Toma v2 uses a dual-font system:

| Element         | Font Family                    | Size  | Weight | Line-Height |
| --------------- | ------------------------------ | ----- | ------ | ----------- |
| **Headings H1** | *Playfair Display*, serif      | 32 px | 600    | 40 px       |
| **Headings H2** | *Playfair Display*, serif      | 24 px | 600    | 32 px       |
| **Headings H3** | *Playfair Display*, serif      | 20 px | 600    | 28 px       |
| **Body Text**   | *Inter*, system-ui, sans-serif | 16 px | 400    | 24 px       |
| **Small Text**  | *Inter*, system-ui, sans-serif | 14 px | 400    | 20 px       |
| **Labels/Tags** | *Inter*, system-ui, sans-serif | 12 px | 500    | 16 px       |
| **Buttons**     | *Inter*, system-ui, sans-serif | 14 px | 600    | 20 px       |

> **Fallbacks:**
>
> * For serif: `Georgia, Times, serif`
> * For sans-serif: `system-ui, -apple-system, BlinkMacSystemFont, sans-serif`

---

## 3. Spacing & Layout

We use an 8 px spacing scale throughout:

* **xxs:** 4 px
* **xs:** 8 px
* **sm:** 16 px
* **md:** 24 px
* **lg:** 32 px
* **xl:** 40 px
* **xxl:** 64 px

**Grid:** 12-column, 24 px gutters
**Container widths:**

* Mobile: 360 px
* Tablet: 768 px
* Desktop: 1,280 px (max content width \~1,024 px)

---

## 4. Border Radius & Elevation

| Element          | Radius | Shadow (Desktop Cards)            |
| ---------------- | ------ | --------------------------------- |
| **Buttons**      | 4 px   | none                              |
| **Inputs**       | 4 px   | none                              |
| **Badges/Tags**  | 2 px   | none                              |
| **Cards/Modals** | 8 px   | 0 px x 2 px 4 px rgba(0,0,0,0.05) |

---

## 5. UI Components

### 5.1 Buttons

```css
.button {
  font-family: Inter, system-ui, sans-serif;
  font-size: 14px; font-weight: 600;
  line-height: 20px;
  padding: 8px 16px; /* sm vertical + md horizontal */
  border-radius: 4px;
  border: none;
  cursor: pointer;
}
.button-primary {
  background-color: #38B6FF;
  color: #FFFFFF;
}
.button-primary:hover {
  background-color: #005F96;
}
.button-secondary {
  background-color: #FFFFFF;
  color: #111827;
  border: 1px solid #D1D5DB;
}
.button-secondary:hover {
  background-color: #F5F5F5;
}
```

### 5.2 Inputs & Search

```css
.input {
  font-family: Inter, system-ui, sans-serif;
  font-size: 16px;
  color: #111827;
  background-color: #F5F5F5;
  border: 1px solid #D1D5DB;
  border-radius: 4px;
  padding: 8px 12px;
}
.input:focus {
  outline: none;
  border-color: #38B6FF;
  box-shadow: 0 0 0 2px rgba(56,182,255,0.3);
}
```

### 5.3 Cards

```css
.card {
  background-color: #FFFFFF;
  border: 1px solid #E5E7EB;
  border-radius: 8px;
  padding: 24px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}
```

### 5.4 Badges / Status Tags

| Type        | BG Color    | Text Color | Border Color |
| ----------- | ----------- | ---------- | ------------ |
| **Active**  | #000000     | #FFFFFF    | —            |
| **Low**     | #FBBF24     | #111827    | —            |
| **Error**   | #EF4444     | #FFFFFF    | —            |
| **Success** | #22C55E     | #FFFFFF    | —            |
| **Outline** | transparent | #6B7280    | #D1D5DB      |

```css
.badge {
  display: inline-block;
  font-size: 12px; font-weight: 500;
  line-height: 16px;
  padding: 2px 8px;
  border-radius: 2px;
}
```

---

## 6. Iconography & Illustrations

* **Icons:** Use a 16 px grid for icons; line-stroke weight \~2 px
* **Common sizes:** 16 px, 20 px, 24 px, 32 px
* **Style:** simple rounded line icons (e.g. Heroicons / Feather)

---

## 7. States & Interactions

| State        | Opacity | BG Color (Light)  | Border Color      |
| ------------ | ------- | ----------------- | ----------------- |
| **Hover**    | —       | #F5F5F5 (buttons) | #D1D5DB (cards)   |
| **Focus**    | —       | —                 | #38B6FF (outline) |
| **Disabled** | 50%     | #F5F5F5           | #E5E7EB           |
| **Loading**  | —       | —                 | show spinner      |

---

## 8. Putting It All Together

1. **Global Reset:**

   ```css
   *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
   html { font-family: Inter, system-ui, sans-serif; color: #111827; background: #FFFFFF; }
   ```
2. **Layout:** Use the 12-column grid with 24 px gutters. Center your main container at max-width 1,024 px.
3. **Components:** Follow the component styles above verbatim.
4. **Accessibility:**

   * Minimum contrast ratios: text vs. BG ≥ 4.5:1
   * Focus rings at least 2 px thick, high-contrast color (#38B6FF)
   * Tap targets ≥ 44 px

---

With this in place, your prototype will match Toma v2’s look exactly—right down to the pixel. Let me know if you need any more details!
