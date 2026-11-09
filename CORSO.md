# Corso Expo: piano e avanzamento

Percorso didattico per imparare Expo / React Native costruendo un'app per Android e web.
Claude aggiorna questo file a fine di ogni modulo o milestone.

## Profilo e scelte
- Conosce JS/TS, **non React**: spiegare i concetti React quando compaiono.
- Linguaggio: **TypeScript**. Route tipizzate di Expo Router e tipi per le risposte dell'API.
- Test: **solo web** per ora (`npx expo start --web`, porta 8081). Android con Expo Go più avanti.
- Metodo: output style **Learning**. Claude scrive il codice di contorno, l'utente scrive la logica
  centrale (`TODO(human)`), poi revisione. Si avanza solo dopo la conferma dell'utente.

## Fase 1: architettura
- [x] **Modulo 1: React per chi sa JS.** Componenti, JSX, props, `useState`, re-render, `useEffect`.
- [x] **Modulo 2: React Native vs React web.** Reconciler e renderer, react-native-web, regole RN
      (testo solo in `<Text>`, `onPress`, `StyleSheet`, Flexbox con `column` di default, niente
      unità), Hermes, JS thread e UI thread, New Architecture (JSI, Fabric, TurboModules).
- [ ] **Modulo 3: cos'è Expo.** SDK `expo-*`, CLI, Metro, Expo Go e development build,
      Expo Router, `app.json`, EAS, prebuild/CNG. ← **PROSSIMO**
- [ ] **Modulo 4: anatomia del progetto.** `npx create-expo-app@latest`, lettura dei file, avvio sul web.

## Fase 2: app "Ricettario" (API TheMealDB, gratuita e senza chiave)
API: `https://www.themealdb.com/api/json/v1/1/` (`search.php?s=`, `lookup.php?i=`, `categories.php`, `filter.php?c=`).

| # | Milestone | Argomenti | Stato |
|---|-----------|-----------|-------|
| 1 | Reset del template + Home statica | componenti core, `StyleSheet`, Flexbox | ☐ |
| 2 | Lista categorie da API | `fetch`, `useEffect`, caricamento ed errore, `FlatList` | ☐ |
| 3 | Tab (Esplora / Preferiti) + stack fino al dettaglio | Expo Router, route dinamiche, `Link`, `useLocalSearchParams` | ☐ |
| 4 | Ricerca + dettaglio con immagine | `TextInput`, debounce, `expo-image`, `ScrollView` | ☐ |
| 5 | Preferiti condivisi e persistiti | Context, hook custom, `AsyncStorage` | ☐ |
| 6 | Tema chiaro/scuro, differenze tra piattaforme | `useColorScheme`, `Platform.OS`, `.web.tsx`, `Alert` sul web | ☐ |
| 7 | Foto "la mia versione" + condivisione | `expo-image-picker`, `expo-sharing`, permessi | ☐ |
| 8 | (Facoltativo) Android con Expo Go | `npx expo start --tunnel` | ☐ |

Struttura prevista: `app/_layout.tsx`, `app/(tabs)/{_layout,index,favorites}.tsx`,
`app/category/[name].tsx`, `app/recipe/[id].tsx`, `lib/api.ts`, `context/FavoritesContext.tsx`.
Verifica a ogni milestone: app nel browser, `npx expo lint`, `npx tsc --noEmit`, commit.

## Punti da rinforzare (dagli esercizi)
- Tipizzare le props destrutturate: `({ etichetta }: Props)`, **non** `({ etichetta: string })`
  (quella sintassi rinomina la variabile).
- Il corpo del componente si riesegue a **ogni** render: una `fetch` lì dentro, seguita da un
  setState, causa un ciclo infinito.
- Stili RN: numeri senza unità, niente scorciatoie (`border` diventa `borderWidth` + `borderColor`),
  `flexDirection: "row"` per affiancare, `StyleSheet.create` fuori dal componente.
- Annidamento: `Pressable` non va dentro `Text`, e le stringhe vanno sempre in `<Text>`.
