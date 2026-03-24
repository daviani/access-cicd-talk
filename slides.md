---
theme: default
title: "Vert en CI, rouge en vrai"
info: "Tests d'accessibilité automatisés, et leurs limites — ApéroWeb Lyon, Mars 2026"
author: Dav
colorSchema: light
aspectRatio: 16/9
canvasWidth: 980
fonts:
  sans: Inter
  mono: Fira Code
transition: slide-left
---

<div class="h-full flex flex-col items-center justify-center relative" style="padding-bottom: 8vh;">
  <p class="mb-6 text-sm font-medium tracking-widest uppercase" style="color: #3B6089;">
    ApéroWeb Lyon — Mars 2026
  </p>

  <OwlLogo :size="64" body-color="#4C566A" eye-color="#ECEFF4" class="mb-4"></OwlLogo>

  <h1 class="text-5xl font-bold text-center leading-tight" style="color: #2E3440;">
    <span style="color: #5A7A3A;">Vert</span> en CI,
    <span style="color: #A5444E;">rouge</span> en vrai
  </h1>

  <p class="mt-4 text-xl text-center" style="color: #3B4252;">
    Tests d'accessibilité automatisés, et leurs limites
  </p>

  <p class="mt-3 text-base" style="color: #4C566A;">
    par Daviani Fillatre
  </p>

  <WaveBackground></WaveBackground>
</div>

<!--
- Ouvrir directement sur la contradiction
- Laisser le titre parler, pas de blabla
- Les vagues posent l'ambiance visuelle
-->

---

<div class="h-full flex items-center px-16">
  <div>
    <h1 class="text-4xl font-bold mb-6" style="color: #2E3440;">Qui je suis</h1>
    <p class="text-2xl mb-4" style="color: #3B4252;">Daviani Fillatre</p>
    <p class="text-lg" style="color: #4C566A;">
      Dev fullstack · 6 ans d'expérience<br>
      .NET, Angular, React, Next.js
    </p>
    <p class="mt-8 text-lg" style="color: #3B6089;">
      Pas expert accessibilité — mais j'ai rendu<br>
      <strong>une app accessible</strong> dans mon précédent poste.
    </p>
  </div>
</div>

<WaveBackground></WaveBackground>

<!--
- Me présenter en 15 secondes max
- Dire que j'ai une vraie expérience pro en accessibilité
- Mais ne pas me vendre comme expert — c'est un dev qui a mis les mains dedans
-->

---

<div class="h-full flex flex-col justify-center px-16">
  <h1 class="text-4xl font-bold mb-8" style="color: #2E3440;">daviani.dev</h1>

  <div class="grid grid-cols-2 gap-8">
    <div>
      <p class="text-lg mb-2 font-semibold" style="color: #3B6089;">Stack</p>
      <p style="color: #4C566A;">
        Monorepo Turborepo<br>
        Next.js 16 · React 19<br>
        Tailwind 4 · TypeScript
      </p>
    </div>
    <div>
      <p class="text-lg mb-2 font-semibold" style="color: #3B6089;">CI/CD</p>
      <p style="color: #4C566A;">
        GitHub Actions<br>
        Vitest · Playwright<br>
        Vercel
      </p>
    </div>
  </div>
</div>

<WaveBackground></WaveBackground>

<!--
- Présenter la stack rapidement — les gens connaissent ces outils
- Ce qui compte c'est le contexte : un vrai projet perso, pas un exercice
-->

---

<div class="h-full flex flex-col justify-center px-16">
  <h1 class="text-4xl font-bold mb-6" style="color: #2E3440;">Pourquoi l'accessibilité ?</h1>

  <p class="text-xl mb-8" style="color: #4C566A;">
    Après avoir rendu des applications accessibles en entreprise,<br>
    j'ai voulu appliquer la même rigueur à <strong>mon site daviani.dev</strong>.
  </p>

  <p class="text-xl" style="color: #4C566A;">
    Objectif : un <strong style="color: #3B6089;">garde-fou dans ma CI</strong><br>
    qui m'empêche de casser l'accessibilité sans m'en rendre compte.
  </p>
</div>

<WaveBackground></WaveBackground>

<!--
- Le déclencheur : l'expérience pro m'a sensibilisé, j'ai voulu transposer sur mon projet perso
- Pas juste Lighthouse → une vraie protection continue dans le pipeline
- Transition : "Alors j'ai construit ça..."
-->

---

<div class="h-full flex flex-col justify-center px-16">
  <h1 class="text-4xl font-bold mb-6" style="color: #2E3440;">Le pipeline</h1>

  <div class="flex items-center gap-4 text-lg" style="color: #4C566A;">
    <div class="px-4 py-2 rounded" style="background: #E5E9F0;">Lint + Types</div>
    <span style="color: #81A1C1;">→</span>
    <div class="px-4 py-2 rounded" style="background: #E5E9F0;">Build</div>
    <span style="color: #81A1C1;">→</span>
    <div class="px-4 py-2 rounded" style="background: #E5E9F0;">Unit Tests</div>
    <span style="color: #81A1C1;">→</span>
    <div class="px-4 py-2 rounded" style="background: #E5E9F0;">E2E</div>
    <span style="color: #81A1C1;">→</span>
    <div class="px-4 py-2 rounded font-bold" style="background: #5A7A3A; color: white;">A11y Tests</div>
    <span style="color: #81A1C1;">→</span>
    <div class="px-4 py-2 rounded" style="background: #E5E9F0;">Deploy</div>
  </div>

  <p class="mt-8 text-base" style="color: #81A1C1;">
    Pas de deploy si les tests d'accessibilité échouent.
  </p>
</div>

<WaveBackground></WaveBackground>

<!--
- Montrer le pipeline de façon visuelle
- Insister : les tests a11y sont un gate — pas de deploy si ça casse
- "Voyons ce qu'il y a dans ces tests..."
-->

---

<div class="h-full flex flex-col justify-center px-12">
  <h1 class="text-3xl font-bold mb-6" style="color: #2E3440;">axe-core : le scan automatique</h1>

```ts {1|3-5|7-9|all}
test('axe-core WCAG 2.1 AA scan', async ({ page }) => {
  const results = await new AxeBuilder({ page })
    .withTags(['wcag2a', 'wcag2aa', 'wcag21a', 'wcag21aa'])
    .analyze();

  const violations = results.violations.filter(
    (v) => v.impact === 'critical' || v.impact === 'serious'
  );

  expect(violations).toHaveLength(0);
});
```

</div>

<!--
- axe-core c'est la base — un scan automatique WCAG
- On filtre par impact critical et serious pour éviter le bruit
- C'est le premier filet de sécurité
- "Mais ça ne suffit pas, on va plus loin..."
-->

---

<div class="h-full flex flex-col justify-center px-12">
  <h1 class="text-3xl font-bold mb-6" style="color: #2E3440;">Critères RGAA testés</h1>

```ts {1-4|6-9|11-14|all}
// Critère 1 — Images : alt text présent et pertinent
const results = await testImagesAccessibility(page);
expect(results.imgWithoutAlt).toHaveLength(0);
expect(results.svgWithoutName).toHaveLength(0);

// Critère 8 — Éléments obligatoires : lang, title, viewport
const lang = await page.locator('html').getAttribute('lang');
expect(lang).toMatch(/^(fr|en)/);
expect(viewport).not.toMatch(/user-scalable\s*=\s*no/i);

// Critère 9 — Structure : h1, hiérarchie, landmarks
expect(results.missingH1).toBe(false);
expect(results.skippedHeadingLevels).toHaveLength(0);
expect(results.missingMainLandmark).toBe(false);
```

</div>

<!--
- On teste les critères RGAA un par un avec des helpers custom
- Images, éléments obligatoires, structure du document
- Chaque critère a son test dédié
- "Et il y en a d'autres..."
-->

---

<div class="h-full flex flex-col justify-center px-12">
  <h1 class="text-3xl font-bold mb-6" style="color: #2E3440;">Au-delà d'axe-core</h1>

```ts {1-3|5-8|10-12|all}
// Navigation clavier — pas de piège au focus
test('no keyboard trap', async ({ page }) => {
  for (let i = 0; i < 50; i++) await page.keyboard.press('Tab');

// Reduced motion — respecter les préférences utilisateur
test('respects prefers-reduced-motion', async ({ page }) => {
  await page.emulateMedia({ reducedMotion: 'reduce' });
  // Vérifie les media queries

// Touch targets — taille minimum 24x24px (WCAG 2.5.8)
test('minimum touch target size', async ({ page }) => {
  if (box.width < 24 || box.height < 24) { /* warn */ }
```

</div>

<!--
- Tests de navigation clavier : on tab 50 fois, pas de piège
- prefers-reduced-motion : on vérifie que les media queries existent
- Touch targets : taille minimum pour le mobile
- "Tout ça passe en CI. Tout est vert. Et pourtant..."
-->

---

<div class="h-full flex flex-col justify-center px-12">
  <h1 class="text-3xl font-bold mb-6" style="color: #2E3440;">Le résultat</h1>

```yaml
# quality.yml — GitHub Actions
jobs:
  accessibility-tests:
    name: Accessibility Tests (RGAA/WCAG)
    needs: quality
    steps:
      - run: pnpm test:a11y
      - uses: actions/upload-artifact@v4
        if: always()  # Upload même en cas d'échec
        with:
          name: accessibility-report
```

  <p class="mt-4 text-2xl font-bold text-center" style="color: #5A7A3A;">
    ✅ Tout est vert.
  </p>
</div>

<!--
- Montrer la config CI — c'est concret, c'est du vrai code
- Le report est uploadé dans tous les cas (if: always())
- "Tout est vert. Mission accomplie ? Pas exactement..."
-->

---

<div class="h-full flex flex-col items-center justify-center px-16">
  <h1 class="text-5xl font-bold text-center mb-8" style="color: #2E3440;">
    <span style="color: #5A7A3A;">Vert</span> partout…<br>
    et pourtant.
  </h1>
</div>

<WaveBackground></WaveBackground>

<!--
- Slide de transition — pause dramatique
- Laisser le silence faire le travail
- "J'en ai parlé à Gabriel..."
-->

---

<div class="h-full flex flex-col justify-center px-16">
  <h1 class="text-3xl font-bold mb-8" style="color: #2E3440;">Ce que les tests ne voient pas</h1>

  <div class="space-y-6 text-xl" style="color: #4C566A;">
    <div v-click>
      <span style="color: #A5444E;">✗</span> La <strong>sémantique</strong> — un alt text peut exister mais être mauvais
    </div>
    <div v-click>
      <span style="color: #A5444E;">✗</span> Le <strong>contexte</strong> — le parcours utilisateur réel avec un lecteur d'écran
    </div>
    <div v-click>
      <span style="color: #A5444E;">✗</span> La <strong>pertinence</strong> — le contenu est-il compréhensible ?
    </div>
    <div v-click>
      <span style="color: #A5444E;">✗</span> Les <strong>cas limites</strong> — dark mode, acronymes, changements de langue
    </div>
  </div>
</div>

<!--
- Clic par clic, révéler les limites
- Les outils testent la présence, pas la qualité
- Un alt="image" passe le test mais n'aide personne
- "Gabriel a testé mon site avec un vrai lecteur d'écran..."
-->

---

<div class="h-full flex flex-col justify-center px-16">
  <h1 class="text-3xl font-bold mb-8" style="color: #2E3440;">L'audit de Gabriel</h1>

  <div class="space-y-5 text-lg" style="color: #4C566A;">
    <div v-click>
      <span style="color: #8B5533;">⚠</span> <strong>"CV"</strong> lu comme <em>"Cheval Vapeur"</em> par VoiceOver
    </div>
    <div v-click>
      <span style="color: #8B5533;">⚠</span> <strong>Contraste insuffisant</strong> en dark mode — ratio 2.21:1 au lieu de 4.5:1
    </div>
    <div v-click>
      <span style="color: #8B5533;">⚠</span> <strong>Placeholders comme labels</strong> — bruit pour les lecteurs d'écran
    </div>
    <div v-click>
      <span style="color: #8B5533;">⚠</span> <strong>Navigation</strong> — parcours incohérent au clavier dans certaines sections
    </div>
  </div>
</div>

<WaveBackground></WaveBackground>

<!--
- Gabriel a testé avec VoiceOver → résultats concrets
- "CV" → "Cheval Vapeur" : le public va rigoler, c'est voulu
- Le contraste dark mode : les outils l'avaient pas vu
- "Aucun de ces bugs n'était détecté par ma CI"
-->

---

<div class="h-full flex flex-col justify-center items-center px-16">
<h1 class="text-3xl font-bold mb-12" style="color: #2E3440;">Le gap</h1>
<table class="text-center">
<tr>
<td class="px-12 text-6xl">🤖</td>
<td class="px-8 text-4xl" style="color: #4C566A;">≠</td>
<td class="px-12 text-6xl">👤</td>
</tr>
<tr>
<td class="pt-4 text-lg font-semibold" style="color: #5A7A3A;">Tests auto</td>
<td></td>
<td class="pt-4 text-lg font-semibold" style="color: #A5444E;">Audit humain</td>
</tr>
<tr>
<td class="pt-2 text-sm" style="color: #4C566A;">Présence, syntaxe, règles</td>
<td></td>
<td class="pt-2 text-sm" style="color: #4C566A;">Sens, contexte, usage</td>
</tr>
</table>
</div>

<WaveBackground></WaveBackground>

<!--
- Slide visuelle simple — le gap entre auto et humain
- Les outils vérifient les règles
- Les humains vérifient le sens
- "Suite à cet audit, j'ai corrigé..."
-->

---

<div class="h-full flex flex-col justify-center px-12">
  <h1 class="text-3xl font-bold mb-6" style="color: #2E3440;">Ce que j'ai corrigé</h1>

```ts {1-4|6-10|all}
// "CV" → aria-label pour les lecteurs d'écran
test('acronyms have accessible labels', async ({ page }) => {
  const results = await testAcronymsAccessibility(page);
  // Vérifie aria-label, title ou <abbr> sur les acronymes

// Dark mode — test de contraste explicite
test('dark mode contrast', async ({ page }) => {
  await page.emulateMedia({ colorScheme: 'dark' });
  const results = await testExplicitContrast(page);
  // Ratio calculé via getComputedStyle
```

  <p class="mt-4 text-base" style="color: #81A1C1;">
    Chaque bug remonté par Gabriel → un nouveau test dans la CI.
  </p>
</div>

<!--
- Chaque bug de l'audit est devenu un test automatisé
- Les acronymes sont maintenant vérifiés
- Le contraste dark mode est testé avec getComputedStyle
- "La boucle est bouclée — mais elle ne se ferme pas toute seule"
-->

---

<div class="h-full flex flex-col justify-center px-12">
  <h1 class="text-3xl font-bold mb-6" style="color: #2E3440;">Les tests enrichis</h1>

```ts {1-3|5-8|10-13|all}
// Changements de langue inline (critère 8.7)
const results = await testInlineLanguageChanges(page);
// Vérifie l'attribut lang sur le contenu étranger

// Placeholders — plus jamais de placeholder seul
const results = await testPlaceholderOnlyInputs(page);
// Chaque input avec placeholder doit avoir un label visible
expect(results.placeholderOnlyInputs).toHaveLength(0);

// Switch de langue — label dans la langue cible
const results = await testLanguageSwitchAccessibility(page);
expect(results.switchMissingAriaLabel).toHaveLength(0);
// L'attribut lang doit correspondre à la langue cible
```

</div>

<!--
- Les tests post-audit : changements de langue, placeholders, switch
- On ne pouvait pas les deviner sans l'audit humain
- "Ça nous amène à la conclusion..."
-->

---

<div class="h-full flex flex-col items-center justify-center px-16 relative" style="padding-bottom: 8vh;">
  <h1 class="text-3xl font-bold mb-8 text-center" style="color: #2E3440;">
    Les outils sont <strong style="color: #5A7A3A;">nécessaires</strong><br>
    mais pas <strong style="color: #A5444E;">suffisants</strong>.
  </h1>

  <div class="space-y-4 text-lg text-center" style="color: #4C566A;">
    <p v-click>Ils t'évitent les erreurs grossières.</p>
    <p v-click>Ils ne remplacent pas un vrai audit humain.</p>
    <p v-click style="color: #5E81AC; font-weight: 600;">
      L'audit nourrit les tests. Les tests protègent l'audit.
    </p>
  </div>

  <WaveBackground></WaveBackground>
</div>

<!--
- Message clé — la phrase à retenir
- Les outils et l'humain se complètent
- L'audit humain nourrit la CI, la CI protège les acquis
- "Et maintenant, Gabriel va vous montrer ce que ça donne en vrai..."
-->

---

<div class="h-full flex flex-col items-center justify-center relative" style="padding-bottom: 8vh;">
  <div class="flex items-center gap-12">
    <div class="flex flex-col items-center">
      <OwlLogo :size="56" body-color="#4C566A" eye-color="#ECEFF4" class="mb-4"></OwlLogo>
      <h1 class="text-4xl font-bold text-center mb-4" style="color: #2E3440;">Place à la démo.</h1>
      <p class="text-xl" style="color: #4C566A;">Gabriel Pillet & Joachim</p>
    </div>
    <div class="flex flex-col items-center">
      <img src="/qr-daviani.png" alt="QR code vers daviani.dev" class="w-32 h-32 mb-2" />
      <p class="text-xs" style="color: #81A1C1;">daviani.dev</p>
    </div>
  </div>

  <WaveBackground></WaveBackground>
</div>

<!--
- Slide de transition vers Gabriel
- Rester sobre — ne pas voler la vedette à la démo
- "Je vous laisse avec Gabriel et Joachim qui vont vous montrer
  ce que ça donne concrètement avec un lecteur d'écran."
-->