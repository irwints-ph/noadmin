# 🧩 Tailwind → Bootstrap 5 Cheat Sheet

---

## 1️⃣ Breakpoints (Mobile-First)

| Tailwind | Min-width | Bootstrap     |
| -------- | --------- | ------------- |
| *(base)* | `<640px`  | *(no prefix)* |
| `sm:`    | ≥640px    | `sm` (≥576px) |
| `md:`    | ≥768px    | `md` ✅        |
| `lg:`    | ≥1024px   | `lg`          |
| `xl:`    | ≥1280px   | `xl`          |
| `2xl:`   | ≥1536px   | `xxl`         |

📌 **Rule**

* Tailwind: `md:...`
* Bootstrap: `...-md-...`

---

## 2️⃣ Margin & Padding

### Same scale in both frameworks

| Value | Size    |
| ----- | ------- |
| `1`   | 0.25rem |
| `2`   | 0.5rem  |
| `3`   | 1rem    |
| `4`   | 1.5rem  |
| `5`   | 3rem    |

### Examples

| Tailwind  | Bootstrap |
| --------- | --------- |
| `m-2`     | `m-2`     |
| `p-4`     | `p-4`     |
| `mx-3`    | `mx-3`    |
| `md:px-4` | `px-md-4` |
| `lg:mt-5` | `mt-lg-5` |

---

## 3️⃣ `space-*` vs `gap-*`

### Tailwind

```tailwind
space-y-4
```

### Bootstrap (no direct equivalent)

```bootstrap
d-flex flex-column gap-4
```

✔ Best replacement
✔ Cleaner than margins

---

## 4️⃣ Flexbox

| Tailwind          | Bootstrap                 |
| ----------------- | ------------------------- |
| `flex`            | `d-flex`                  |
| `flex-col`        | `flex-column`             |
| `flex-row`        | `flex-row`                |
| `md:flex-row`     | `flex-md-row`             |
| `items-center`    | `align-items-center`      |
| `items-end`       | `align-items-end`         |
| `justify-between` | `justify-content-between` |
| `justify-end`     | `justify-content-end`     |
| `flex-1`          | `flex-grow-1`             |

---

## 5️⃣ Grid & Columns

### Tailwind grid

```tailwind
grid grid-cols-1 md:grid-cols-2
```

### Bootstrap grid

```bootstrap
row
col-12 col-md-6
```

---

### 1/3 – 2/3 layout (desktop)

| Tailwind                 | Bootstrap           |
| ------------------------ | ------------------- |
| `md:grid-cols-[1fr_2fr]` | `col-md-4 col-md-8` |

---

### Exact percentages (Bootstrap only)

```bootstrap
col-md-auto
style="flex: 0 0 35%"
```

---

## 6️⃣ Visibility

| Tailwind         | Bootstrap          |
| ---------------- | ------------------ |
| `hidden`         | `d-none`           |
| `md:block`       | `d-md-block`       |
| `hidden md:flex` | `d-none d-md-flex` |
| `sm:hidden`      | `d-sm-none`        |

---

## 7️⃣ Containers

| Bootstrap class | Behavior      |
| --------------- | ------------- |
| `container`     | Always fixed  |
| `container-md`  | Fixed ≥768px  |
| `container-lg`  | Fixed ≥992px  |
| `container-xl`  | Fixed ≥1200px |

✔ Use `container-md` for **desktop-only container**

---

## 8️⃣ Alignment tricks (very common)

### Bottom-align columns on desktop

```bootstrap
row align-items-md-end
```

---

### Search left, buttons right

```bootstrap
d-flex
align-items-center
```

```bootstrap
flex-grow-1   /* input */
```

---

### Right-aligned content

```bootstrap
justify-content-end
```

---

## 9️⃣ Buttons (clean + modern)

### Green text, no border, no background

```bootstrap
btn text-success border-0
```

---

### Hide on mobile

```bootstrap
d-none d-md-inline-block
```

---

## 🔟 Your frequent pattern

### Tailwind

```tailwind
m-2 p-4 space-y-4
```

### Bootstrap

```bootstrap
m-2 p-4 d-flex flex-column gap-4
```

---

## 🧠 Mental Model

* **Tailwind = utilities first**
* **Bootstrap = layout + utilities**
* Use:

  * `row / col-*` for structure
  * `d-flex + gap-*` for spacing
  * `*-md-*` for desktop-only changes

---

Great question — this is a **core concept** and once it clicks, Tailwind vs Bootstrap makes *way* more sense.

---

## What does **“utilities-first”** mean?

**Utilities-first** means:

> You build your UI almost entirely by composing **small, single-purpose CSS classes** directly in your HTML/JSX — instead of writing custom CSS or semantic components.

Each class does **one thing only**.

---

## Example (Tailwind – utilities-first)

```html
<div class="flex items-center justify-between p-4 bg-white rounded-lg shadow">
```

Each class = **one rule**:

| Class             | What it does        |
| ----------------- | ------------------- |
| `flex`            | display: flex       |
| `items-center`    | align-items: center |
| `justify-between` | space between       |
| `p-4`             | padding             |
| `bg-white`        | background          |
| `rounded-lg`      | border radius       |
| `shadow`          | box shadow          |

🧩 You **compose** styles instead of defining a component.

---

## Contrast: Component-first (Bootstrap’s origin)

Bootstrap started as **component-first**:

```html
<button class="btn btn-primary btn-lg">
```

Here:

* `.btn` = base styles
* `.btn-primary` = predefined color
* `.btn-lg` = size

You pick from **prebuilt opinions**.

---

## Why Tailwind is utilities-first

Tailwind **does not ship UI components**.
It ships **CSS primitives**.

You build:

* Buttons
* Cards
* Layouts

…yourself, by combining utilities.

---

## Bootstrap today (hybrid)

Bootstrap is now **hybrid**:

* **Component-first**

  * `btn`, `card`, `modal`, `navbar`
* **Utility-heavy**

  * `d-flex`
  * `gap-3`
  * `p-4`
  * `align-items-center`
  * `justify-content-between`

So when converting:

> Tailwind → Bootstrap
> you often replace **many small utilities** with **fewer structural classes**.

---

## Example: Same layout, different philosophies

### Tailwind

```html
<div class="flex flex-col md:flex-row gap-4 p-4">
```

### Bootstrap

```html
<div class="d-flex flex-column flex-md-row gap-4 p-4">
```

Same utilities — Bootstrap just uses **longer names**.

---

## When utilities-first shines

✔ Fast prototyping
✔ Highly custom layouts
✔ Design systems
✔ No CSS files
✔ Easy responsive tweaks

---

## When component-first shines

✔ Consistent UI
✔ Faster onboarding
✔ Less JSX clutter
✔ Prebuilt accessibility

---

## Your mental shortcut

* **Tailwind** = Lego bricks
* **Bootstrap** = Lego sets + bricks

You can:

* Use only bricks
* Use only sets
* Mix both (what you’re doing now 👍)

---

If you want, I can show:

* ❌ a *bad* utility-first example
* ✅ a *good* utility-first example
* 🔁 how to “think utilities-first” in Bootstrap

Just tell me.
