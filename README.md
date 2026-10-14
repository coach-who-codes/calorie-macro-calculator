# Amit Calorie App

A calorie and macro calculator for gym clients that installs on a phone like an app. Enter weight, height, age, gender, activity level and goal (fat loss, maintenance or muscle gain) to get daily calories, protein, carbs and fat, plus a per-meal split.

The app is `index.html` plus a few small files that make it installable: `manifest.webmanifest` (name and icons), `sw.js` (offline support) and `icons/`. There is no build step and no dependencies apart from the Google Fonts it loads.

## Put it online (one time)

1. On GitHub open **Settings → Pages**.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, pick `claude/gym-calorie-macro-calculator-ub3gcs` and `/ (root)`, then **Save**.
3. After a minute or two the app is live at `https://gymboy-will-code.github.io/my-code/`.

## Install on a phone

- **Android (Chrome):** open the link and tap the **Install** button on the page, or use ⋮ → **Install app** / **Add to Home screen**.
- **iPhone (Safari):** open the link, tap **Share**, then **Add to Home Screen**.

Once installed it opens from the home screen in its own window and works without internet.

After changing `index.html`, the manifest or the icons, bump `CACHE` in `sw.js` (for example `amit-calorie-v2`) so installed phones pick up the new version.

## How it calculates

1. **BMR** with Mifflin-St Jeor: `10 × kg + 6.25 × cm − 5 × age + 5` (men) or `− 161` (women).
2. **Maintenance (TDEE)** = BMR × activity factor (1.2 / 1.375 / 1.55 / 1.725 / 1.9).
3. **Goal:** fat loss −20%, maintenance ±0, muscle gain +10%. Fat loss is floored at 1,500 kcal (men) / 1,200 kcal (women).
4. **Protein:** 2.0 / 1.6 / 1.8 g per kg for fat loss / maintenance / muscle gain. Above BMI 27 it uses the weight at BMI 27 for that height.
5. **Fat:** 25% of calories (30% at maintenance), at least 0.6 g per kg.
6. **Carbs:** the remaining calories.

To change any of these, edit the constants at the top of the main `<script>` block in `index.html` (`ACTIVITY`, `GOALS`, `MIN_CUT_KCAL`, `PROTEIN_BMI_CAP`, `MIN_FAT_PER_KG`).

A client's last entries are saved in their own browser, so the app remembers them next time.
