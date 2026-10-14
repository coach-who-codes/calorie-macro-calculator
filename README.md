# Calorie & Macro Calculator

A single-page calculator for gym clients. Enter weight, height, age, gender, activity level and goal (fat loss, maintenance or muscle gain) to get daily calories, protein, carbs and fat, plus a per-meal split.

Everything lives in `index.html`: no build step and no dependencies apart from the Google Fonts it loads. Open it in a browser, or host it with GitHub Pages (Settings → Pages → deploy from the default branch).

## How it calculates

1. **BMR** with Mifflin-St Jeor: `10 × kg + 6.25 × cm − 5 × age + 5` (men) or `− 161` (women).
2. **Maintenance (TDEE)** = BMR × activity factor (1.2 / 1.375 / 1.55 / 1.725 / 1.9).
3. **Goal:** fat loss −20%, maintenance ±0, muscle gain +10%. Fat loss is floored at 1,500 kcal (men) / 1,200 kcal (women).
4. **Protein:** 2.0 / 1.6 / 1.8 g per kg for fat loss / maintenance / muscle gain. Above BMI 27 it uses the weight at BMI 27 for that height.
5. **Fat:** 25% of calories (30% at maintenance), at least 0.6 g per kg.
6. **Carbs:** the remaining calories.

To change any of these, edit the constants at the top of the `<script>` block (`ACTIVITY`, `GOALS`, `MIN_CUT_KCAL`, `PROTEIN_BMI_CAP`, `MIN_FAT_PER_KG`).

## Customising

- Put your gym's name in place of "Gym nutrition" (the small line above the heading).
- A client's last entries are saved in their own browser, so the page remembers them next time.
