---
title: TypeScript ని ఉపయోగించడం
re: https://github.com/reactjs/react.dev/issues/5960
---

<Intro>

TypeScript అనేది JavaScript కోడ్‌బేస్‌లకు టైప్ డెఫినిషన్‌లను జోడించడానికి ఒక ప్రసిద్ధ మార్గం. TypeScript [JSX ని సపోర్ట్ చేస్తుంది](/learn/writing-markup-with-jsx) మరియు మీరు మీ ప్రాజెక్ట్‌కి [`@types/react`](https://www.npmjs.com/package/@types/react) మరియు [`@types/react-dom`](https://www.npmjs.com/package/@types/react-dom) ను చేర్చడం ద్వారా పూర్తి React Web సపోర్ట్ని పొందవచ్చు.

</Intro>

<YouWillLearn>

* [TypeScript లో React కాంపోనెంట్లను ఎలా రాయడం](/learn/typescript#typescript-with-react-components)
* [Hooks తో టైప్ ఉదాహరణలు](/learn/typescript#example-hooks)
* [`@types/react` నుండి సాధారణ టైప్స్](/learn/typescript#useful-types)
* [మరింత నేర్చుకోవడానికి రిసోర్సెస్](/learn/typescript#further-learning)

</YouWillLearn>

## ఇన్‌స్టాలేషన్ {/*installation*/}

<<<<<<< HEAD
అన్ని [ప్రొడక్షన్-గ్రేడ్ React ఫ్రేమ్‌వర్క్‌లు](/learn/start-a-new-react-project#full-stack-frameworks) TypeScript ని ఉపయోగించడం కోసం సపోర్ట్ను అందిస్తాయి. ఇన్‌స్టాలేషన్ కోసం ఫ్రేమ్‌వర్క్ యొక్క ప్రత్యేక గైడ్‌ను అనుసరించండి:
=======
All [production-grade React frameworks](/learn/creating-a-react-app#full-stack-frameworks) offer support for using TypeScript. Follow the framework specific guide for installation:
>>>>>>> 2534424ec6c433cc2c811d5a0bd5a65b75efa5f0

- [Next.js](https://nextjs.org/docs/app/building-your-application/configuring/typescript)
- [Remix](https://remix.run/docs/en/1.19.2/guides/typescript)
- [Gatsby](https://www.gatsbyjs.com/docs/how-to/custom-configuration/typescript/)
- [Expo](https://docs.expo.dev/guides/typescript/)

### ఇప్పటికే ఉన్న React ప్రాజెక్ట్‌కి TypeScript ని జోడించడం {/*adding-typescript-to-an-existing-react-project*/}

React యొక్క టైప్ డెఫినిషన్ల లేటెస్ట్ వెర్షన్ను ఇన్‌స్టాల్ చేయడానికి:

<TerminalBlock>
npm install --save-dev @types/react @types/react-dom
</TerminalBlock>

మీ `tsconfig.json` లో, క్రింది కంపైలర్ ఆప్షన్స్ ని సెట్ చేయాలి:

1. [`lib`](https://www.typescriptlang.org/tsconfig/#lib) లో `dom` ఉండాలి (గమనిక: ఎలాంటి `lib` ఆప్షన్ స్పెసిఫ్య్ చేయలేదు అంటే, `dom` డిఫాల్ట్ గా ఉంటుంది).
2. [`jsx`](https://www.typescriptlang.org/tsconfig/#jsx) ని తప్పనిసరిగా వెలిడ్ అయ్యే ఆప్షన్లలో ఒకదానికి సెట్ చేయాలి. చాలా అప్లికేషన్స్‌కి `preserve` సరిపోతుంది.
  మీరు లైబ్రరీని పబ్లిష్ చేస్తున్నట్లు అయితే, ఎలాంటి వేల్యూ ను ఎంచుకోవాలో తెలుసుకోవడానికి [`jsx` డాక్యుమెంటేషన్](https://www.typescriptlang.org/tsconfig/#jsx) ను సంప్రదించండి.

## TypeScript లో React కాంపోనెంట్లను ఎలా రాయడం {/*typescript-with-react-components*/}

<Note>

JSX ని కలిగి ఉన్న ప్రతి ఫైల్ తప్పనిసరిగా `.tsx` ఫైల్ ఎక్స్‌టెన్షన్‌ ని ఉపయోగించాలి. ఇది TypeScript స్పెసిఫిక్ ఎక్స్‌టెన్షన్‌, ఇది ఈ ఫైల్‌లో JSX ఉందని TypeScript కు తెలియజేస్తుంది.

</Note>

React లో TypeScript వ్రాయడం అనేది React లో JavaScript వ్రాయడముతో సమానం. ఒక కాంపోనెంట్‌తో పని చేస్తున్నప్పుడు ముఖ్యమైన తేడా ఏమిటంటే మీరు మీ కాంపోనెంట్ యొక్క props కోసం టైప్స్ ను అందించవచ్చు. ఈ టైప్స్ అనేవి సరిగ్గా ఉన్నాయో లేదో చెక్ చేయడానికి మరియు మీ ఎడిటర్ కు ఇన్లైన్ డాక్యుమెంటేషన్ ని అందించడానికి ఉపయోగించవచ్చు.

[క్విక్ స్టార్ట్](/learn) గైడ్ నుండి [`MyButton` కాంపోనెంట్](/learn#components) తీసుకుని, బటన్ కోసం `title` ను వివరిస్తున్న టైప్ ని జోడించవచ్చు:

<Sandpack>

```tsx src/App.tsx active
function MyButton({ title }: { title: string }) {
  return (
    <button>{title}</button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>నా యాప్‌కి స్వాగతం</h1>
      <MyButton title="నేను ఒక బటన్‌ ని" />
    </div>
  );
}
```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```
</Sandpack>

 <Note>

ఈ శాండ్‌బాక్స్‌లు TypeScript కోడ్‌ ను హేండిల్ చేయగలవు, కానీ అవి టైప్-చెకర్‌ ను రన్ చేయలేవు. అంటే, మీరు TypeScript శాండ్బాక్స్లో సవరణలు చేయవచ్చు, కానీ మీకు ఏదైనా టైప్ ఎర్రర్స్ లేదా హెచ్చరికలు రావు. టైప్-చెకింగ్ పొందడానికి, మీరు [TypeScript ప్లేగ్రౌండ్](https://www.typescriptlang.org/play) ను లేదా మరింత ఫుల్లీ-ఫీచర్డ్ ఆన్లైన్ శాండ్బాక్స్ ను ఉపయోగించవచ్చు.

</Note>

ఈ ఇన్లైన్ సింటాక్స్ అనేది ఒక కాంపోనెంట్‌కు టైప్స్ ని అందించడానికి అత్యంత సులభమైన మార్గం, కానీ మీరు కొన్ని ఫీల్డ్స్‌ను వివరిస్తూ ప్రారంభించినప్పుడు ఇది గందరగోళంగా మారవచ్చు. దీనికి బదులుగా, మీరు కాంపోనెంట్ యొక్క props ను వివరిచేందుకు `interface` లేదా `type` ని ఉపయోగించవచ్చు:

<Sandpack>

```tsx src/App.tsx active
interface MyButtonProps {
  /** బటన్ లోపల చూపించాల్సిన టెక్స్ట్ */
  title: string;
  /** బటన్‌ తో ఇంటరాక్ట్ అవవచ్చా */
  disabled: boolean;
}

function MyButton({ title, disabled }: MyButtonProps) {
  return (
    <button disabled={disabled}>{title}</button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>నా యాప్‌కి స్వాగతం</h1>
      <MyButton title="నేను డిసేబుల్డ్ బటన్‌ ని" disabled={true}/>
    </div>
  );
}
```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```

</Sandpack>

మీ కాంపోనెంట్ యొక్క props ను వివరిస్తున్న టైప్ అవసరమైనంత సులభంగా లేదా క్లిష్టంగా ఉండవచ్చు, కానీ అవి `type` లేదా `interface` తో వివరించబడిన ఆబ్జెక్ట్ టైప్ అయి ఉండాలి. TypeScript ఆబ్జెక్ట్స్ ను ఎలా వివరిస్తుందో మీరు [ఆబ్జెక్ట్ టైప్స్](https://www.typescriptlang.org/docs/handbook/2/objects.html) లో నేర్చుకోవచ్చు కానీ మీరు [యూనియన్ టైప్స్](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types) ను కూడా props గా వివరిస్తూ ఉపయోగించడం గురించి ఆసక్తి చూపవచ్చు, ఇది కొన్ని విభిన్న టైప్లలో ఒకటి కావచ్చు మరియు మరింత ఆధునిక యూజ్ కేసుల కోసం [టైప్స్ నుండి టైప్లను సృష్టించడం](https://www.typescriptlang.org/docs/handbook/2/types-from-types.html) అనే గైడ్ ఉపయోగపడుతుంది.

## Hooks తో టైప్ ఉదాహరణలు {/*example-hooks*/}

`@types/react` నుండి టైప్ డెఫినిషన్‌లు బిల్ట్-ఇన్ Hooks కోసం టైప్లను కలిగి ఉంటాయి, కాబట్టి మీరు వాటిని ఎలాంటి అదనపు సెటప్ లేకుండానే మీ కాంపోనెంట్లలో ఉపయోగించవచ్చు. అవి మీ కాంపోనెంట్ లో మీరు వ్రాసే కోడ్ ను పరిగణనలోకి తీసుకుంటాయి, కాబట్టి చాలా సార్లు మీరు [ఇన్ఫెరెడ్ టైప్స్](https://www.typescriptlang.org/docs/handbook/type-inference.html) పొందుతారు మరియు సాధారణంగా టైప్స్ ను ఇవ్వడానికి ఎటువంటి సమస్యలు ఎదుర్కొనవలసిన అవసరం లేదు.

అయితే, Hooks కోసం టైప్స్ ను ఎలా అందించాలో కొన్ని ఉదాహరణలను చూద్దాం.

### `useState` {/*typing-usestate*/}

[`useState` Hook](/reference/react/useState) ఇనీషియల్ state గా ఇవ్వబడిన వేల్యూ ను రీ-యూజ్ చేసుకొని ఆ వేల్యూ యొక్క టైప్ ఏమిటి అని నిర్ధారిస్తుంది. ఉదాహరణకు:

```ts
// టైప్ ను "boolean" గా సూచిస్తుంది
const [enabled, setEnabled] = useState(false);
```

ఇది `enabled` కు `boolean` టైప్ ను అసైన్ చేస్తుంది, మరియు `setEnabled` అనేది `boolean` ఆర్గుమెంట్ ను స్వీకరించే ఫంక్షన్ లేదా `boolean` ను రిటర్న్ చేసే ఫంక్షన్ అవుతుంది. మీరు state కోసం టైప్ ను ఎక్సప్లిసిట్ గా ఇవ్వాలనుకుంటే, మీరు `useState` కాల్ కు టైప్ ఆర్గుమెంట్ ను ఇవ్వవచ్చు:

```ts
// టైప్ ను "boolean" కి ఎక్సప్లిసిట్ గా సెట్ చేయండి
const [enabled, setEnabled] = useState<boolean>(false);
```

ఇది ఈ సందర్భంలో అంతగా ఉపయోగకరమైనది కాదు, కానీ మీరు `type` ను ఇవ్వాలనుకునే సాధారణ సందర్భం యూనియన్ టైప్ ఉన్నప్పుడు. ఉదాహరణకు, `status` ఇక్కడ కొన్ని వేర్వేరు స్ట్రింగ్స్ లో ఒకటి కావచ్చు:

```ts
type Status = "idle" | "loading" | "success" | "error";

const [status, setStatus] = useState<Status>("idle");
```

లేదా, [ప్రిన్సిపుల్స్ ఫర్ స్తృక్చరింగ్ state](/learn/choosing-the-state-structure#principles-for-structuring-state) లో సిఫారసు చేసినట్లు, మీరు సంబంధిత state ను ఒక ఆబ్జెక్ట్ గా గ్రూప్ చేసి, వేర్వేరు అవకాశాలను ఆబ్జెక్ట్ టైప్స్ ద్వారా వివరించవచ్చు:

```ts
type RequestState =
  | { status: 'idle' }
  | { status: 'loading' }
  | { status: 'success', data: any }
  | { status: 'error', error: Error };

const [requestState, setRequestState] = useState<RequestState>({ status: 'idle' });
```

### `useReducer` {/*typing-usereducer*/}

[`useReducer` Hook](/reference/react/useReducer) ఒక కాంప్లెక్స్ Hook, ఇది ఒక reducer ఫంక్షన్ మరియు ఒక ఇనీషియల్ state ను తీసుకుంటుంది. reducer ఫంక్షన్ కోసం టైప్స్ అనేవి ఇనీషియల్ state నుండి అంచనా వేయబడతాయి. మీరు `useReducer` కాల్ కు టైప్ ఆర్గుమెంట్ ను ఇస్తూ state కోసం టైప్ ను ప్రొవైడ్ చేయవచ్చు, కానీ ఇనీషియల్ state పై టైప్ సెట్ చేయడం మంచిది:

<Sandpack>

```tsx src/App.tsx active
import {useReducer} from 'react';

interface State {
   count: number
};

type CounterAction =
  | { type: "reset" }
  | { type: "setCount"; value: State["count"] }

const initialState: State = { count: 0 };

function stateReducer(state: State, action: CounterAction): State {
  switch (action.type) {
    case "reset":
      return initialState;
    case "setCount":
      return { ...state, count: action.value };
    default:
      throw new Error("తెలియని ఆక్షన్");
  }
}

export default function App() {
  const [state, dispatch] = useReducer(stateReducer, initialState);

  const addFive = () => dispatch({ type: "setCount", value: state.count + 5 });
  const reset = () => dispatch({ type: "reset" });

  return (
    <div>
      <h1>నా కౌంటర్‌కి స్వాగతం</h1>

      <p>కౌంట్: {state.count}</p>
      <button onClick={addFive}>5 ని యాడ్ చేయండి</button>
      <button onClick={reset}>రీసెట్</button>
    </div>
  );
}

```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```

</Sandpack>


మేము TypeScript ను కొన్ని కీలక ప్రదేశాలలో ఉపయోగిస్తున్నాము:

 - `interface State` reducer యొక్క state షేప్ ని డిస్క్రైబ్ చేస్తుంది.
 - `type CounterAction` reducer కు dispatch చేసే వేర్వేరు actions ను డిస్క్రైబ్ చేస్తుంది.
 - `const initialState: State` ఇనీషియల్ state కు టైప్ ను అందిస్తుంది, మరియు అదే టైప్ `useReducer` ద్వారా డిఫాల్ట్ గా ఉపయోగించబడుతుంది.
 - `stateReducer(state: State, action: CounterAction): State` reducer ఫంక్షన్ యొక్క అర్గుమెంత్స్ మరియు రిటర్న్ వేల్యూ కు టైప్స్ ను సెట్ చేస్తుంది.

`initialState` పై టైప్ని సెట్ చేయడానికి మరింత ఎక్స్ప్లిసిట్ ఆల్టర్నేటివ్ `useReducer` కు టైప్ ఆర్గుమెంట్ ను అందించడం:

```ts
import { stateReducer, State } from './your-reducer-implementation';

const initialState = { count: 0 };

export default function App() {
  const [state, dispatch] = useReducer<State>(stateReducer, initialState);
}
```

### `useContext` {/*typing-usecontext*/}

[`useContext` Hook](/reference/react/useContext) props ను కాంపోనెంట్స్ ద్వారా పంపకుండా, డేటా ను కాంపోనెంట్ ట్రీ లోకి పంపించడానికి ఒక పద్ధతి. ఇది ఒక provider కాంపోనెంట్ ను సృష్టించడం ద్వారా ఉపయోగించబడుతుంది మరియు తరచుగా ఒక Hook ను సృష్టించడం ద్వారా చైల్డ్ కాంపోనెంట్లో వేల్యూ ను వినియోగించడానికి ఉపయోగించబడుతుంది.

context ద్వారా ప్రొవైడ్ చేయబడిన వేల్యూ యొక్క టైప్, `createContext` కాల్ కు పంపబడిన వేల్యూ నుండి అంచనా వేయబడుతుంది:

<Sandpack>

```tsx src/App.tsx active
import { createContext, useContext, useState } from 'react';

type Theme = "light" | "dark" | "system";
const ThemeContext = createContext<Theme>("system");

const useGetTheme = () => useContext(ThemeContext);

export default function MyApp() {
  const [theme, setTheme] = useState<Theme>('light');

  return (
    <ThemeContext value={theme}>
      <MyComponent />
    </ThemeContext>
  )
}

function MyComponent() {
  const theme = useGetTheme();

  return (
    <div>
      <p>ప్రస్తుత థీమ్: {theme}</p>
    </div>
  )
}
```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```

</Sandpack>

మీకు అర్థమయ్యే డిఫాల్ట్ వేల్యూ ఉన్నప్పుడు ఈ టెక్నిక్ పని చేస్తుంది - కానీ అప్పుడప్పుడు మీకు డిఫాల్ట్ వేల్యూ లేని సందర్భాలు ఉంటాయి, మరియు ఆ సందర్భాలలో `null` ఒక డిఫాల్ట్ వేల్యూ గా సరైనదిగా భావించవచ్చు. అయితే, టైప్-సిస్టం మీ కోడ్‌ ను అర్థం చేసుకునేలా చేయడానికి, మీరు `createContext` లో `ContextShape | null` ను ఎక్సప్లిసిట్ గా సెట్ చేయాలి.

ఇది `| null` ను context కన్స్యూమర్ల టైప్ లో నుండి తొలగించాల్సిన సమస్యను కలిగిస్తుంది. మా సిఫార్సు ఏమిటంటే, Hook ఒక రన్‌టైమ్ చెక్ చేసి, అది లేకపోతే ఒక ఎర్రర్ ని throw చేస్తుంది:

```js {5, 16-20}
import { createContext, useContext, useState, useMemo } from 'react';

// ఇది సింపుల్ ఉదాహరణ, కానీ మీరు ఇక్కడ మరింత క్లిష్టమైన ఆబ్జెక్ట్ ను ఊహించవచ్చు
type ComplexObject = {
  kind: string
};

// సరైన డిఫాల్ట్ వేల్యూ ను ప్రతిబింబించడానికి, `| null` టైప్ తో context సృష్టించబడింది.
const Context = createContext<ComplexObject | null>(null);

// `| null` అనేది Hook లోని చెక్ ద్వారా తొలగించబడుతుంది.
const useGetComplexObject = () => {
  const object = useContext(Context);
  if (!object) { throw new Error("useGetComplexObject ఒక provider లోనే ఉపయోగించాలి.") }
  return object;
}

export default function MyApp() {
  const object = useMemo(() => ({ kind: "complex" }), []);

  return (
    <Context value={object}>
      <MyComponent />
    </Context>
  )
}

function MyComponent() {
  const object = useGetComplexObject();

  return (
    <div>
      <p>ప్రస్తుత ఆబ్జెక్ట్: {object.kind}</p>
    </div>
  )
}
```

### `useMemo` {/*typing-usememo*/}

<Note>

[React Compiler](/learn/react-compiler) ఆటోమేటిక్ గా వాల్యూస్ మరియు ఫంక్షన్లను మెమోరైజ్ చేస్కుంటుంది, మాన్యువల్ `useMemo` కాల్స్ అవసరాన్ని తగ్గిస్తుంది. మీరు మెమోరైజేషన్‌ ని ఆటోమేటిక్ గా నిర్వహించడానికి కంపైలర్‌ ని ఉపయోగించవచ్చు.

</Note>

[`useMemo`](/reference/react/useMemo) Hook ఒక ఫంక్షన్ కాల్ నుండి ఒక మేమోరైజ్డ్ వేల్యూ ను సృష్టిస్తుంది/రీ-అక్సెస్ చేస్తుంది, 2వ పారామీటర్‌గా పంపబడిన డిపెండెన్సీలు మారినప్పుడు మాత్రమే ఫంక్షన్ రీ-రన్ అవుతుంది. Hook ను కాల్ చేయడం వలన వచ్చిన రిజల్ట్ అనేది మొదటి పారామీటర్‌ లోని ఫంక్షన్ నుండి రిటర్న్ అయిన వాల్యూ ద్వారా అంచనా వేయబడుతుంది. మీరు మరింత ఎక్స్ప్లిసిట్ గా టైప్ ఆర్గుమెంట్ ను Hook కు ప్రొవైడ్ చేయవచ్చు.

```ts
// visibleTodos యొక్క టైప్, filterTodos యొక్క రిటర్న్ వేల్యూ నుండి ఊహించబడుతుంది.
const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
```


### `useCallback` {/*typing-usecallback*/}

<Note>

[React Compiler](/learn/react-compiler) ఆటోమేటిక్ గా వాల్యూస్ మరియు ఫంక్షన్లను మెమోరైజ్ చేస్కుంటుంది, మాన్యువల్ `useCallback` కాల్స్ అవసరాన్ని తగ్గిస్తుంది. మీరు మెమోరైజేషన్‌ ని ఆటోమేటిక్ గా నిర్వహించడానికి కంపైలర్‌ ని ఉపయోగించవచ్చు.

</Note>

[`useCallback`](/reference/react/useCallback) రెండవ పారామీటర్లోకి పంపబడిన డిపెండెన్సీలు ఒకేలా ఉన్నంత వరకు ఒక ఫంక్షన్‌కు స్టేబుల్ రిఫరెన్స్ ను అందిస్తాయి. `useMemo` లాగా, ఫంక్షన్ యొక్క టైప్ మొదటి పారామీటర్లోని ఫంక్షన్ యొక్క రిటర్న్ వేల్యూ నుండి అంచనా వేయబడుతుంది, మరియు మీరు మరింత ఎక్స్ప్లిసిట్ గా టైప్ ఆర్గుమెంట్ ను Hook కు ప్రొవైడ్ చేయవచ్చు.

```ts
const handleClick = useCallback(() => {
  // ...
}, [todos]);
```

TypeScript strict mode లో పని చేస్తున్నప్పుడు `useCallback` లో మీ కాల్ బ్యాక్ లోని పారామీటర్స్ కు టైప్స్ ను చేర్చాలి. ఇది ఎందుకంటే కాల్ బ్యాక్ యొక్క టైప్ అనేది ఫంక్షన్ యొక్క రిటర్న్ వేల్యూ నుండి అంచనా వేయబడుతుంది, మరియు పారామీటర్స్ లేకుండా టైప్ అనేది పూర్తిగా అర్థం కాదు.

మీ కోడ్-స్టైల్ ప్రిఫరెన్సెస్ పై ఆధారపడి, కాల్ బ్యాక్ ను డిఫైన్ చేసే సమయంలో ఈవెంట్ హ్యాండ్లర్ కోసం టైప్ ను అందించడానికి React టైప్స్ నుండి `*EventHandler` ఫంక్షన్స్ ను ఉపయోగించవచ్చు:

```ts
import { useState, useCallback } from 'react';

export default function Form() {
  const [value, setValue] = useState("నన్ను మార్చు");

  const handleChange = useCallback<React.ChangeEventHandler<HTMLInputElement>>((event) => {
    setValue(event.currentTarget.value);
  }, [setValue])

  return (
    <>
      <input value={value} onChange={handleChange} />
      <p>వేల్యూ: {value}</p>
    </>
  );
}
```

## ఉపయోగకరమైన టైప్స్ {/*useful-types*/}

`@types/react` ప్యాకేజ్ నుండి చాలా విస్తృతమైన టైప్స్ సెట్ వస్తుంది, React మరియు TypeScript ఎలా ఇంటరాక్ట్ అవుతాయి అనే దాని గురించి మీరు సౌకర్యంగా భావించినప్పుడు ఇది చదవడం విలువైనది. మీరు వాటిని [DefinitelyTyped లో React యొక్క ఫోల్డర్ లో](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/react/index.d.ts) కనుగొనవచ్చు. ఇక్కడ మేము కొన్ని సాధారణంగా ఉపయోగించే టైప్స్ ను కవర్ చేస్తాము.

### DOM ఈవెంట్స్ {/*typing-dom-events*/}

React లో DOM ఈవెంట్స్ తో పని చేస్తున్నప్పుడు, ఈవెంట్ యొక్క టైప్ అనేది ఈవెంట్ హ్యాండ్లర్ నుండి తరచుగా అంచనా వేయబడుతుంది. అయితే, ఒక ఫంక్షన్ ను ఈవెంట్ హ్యాండ్లర్ కు పంపించడానికి ఎక్స్ట్రాక్ట్ చేయాలనుకుంటే, మీరు ఈవెంట్ యొక్క టైప్ ను ఎక్సప్లిసిట్ గా సెట్ చేయాలి.

<Sandpack>

```tsx src/App.tsx active
import { useState } from 'react';

export default function Form() {
  const [value, setValue] = useState("నన్ను మార్చు");

  function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
    setValue(event.currentTarget.value);
  }

  return (
    <>
      <input value={value} onChange={handleChange} />
      <p>వేల్యూ: {value}</p>
    </>
  );
}
```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```

</Sandpack>

React టైప్స్ లో చాలా రకాల ఈవెంట్స్ అందుబాటులో ఉన్నాయి - పూర్తి లిస్ట్ ను [ఇక్కడ](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/b580df54c0819ec9df62b0835a315dd48b8594a9/types/react/index.d.ts#L1247C1-L1373) చూడవచ్చు, ఇవి [DOM నుండి పాపులర్ ఈవెంట్స్](https://developer.mozilla.org/en-US/docs/Web/Events) పై ఆధారపడి ఉంటాయి.

మీరు వెతుకుతున్న టైప్ ను నిర్ణయించేటప్పుడు మీరు ముందుగా మీరు ఉపయోగిస్తున్న ఈవెంట్ హ్యాండ్లర్ కోసం హోవర్ ఇన్ఫర్మేషన్ ని చూడవచ్చు, ఇది ఈవెంట్ టైప్ ని చూపిస్తుంది.

ఈ లిస్టులో లేని ఈవెంట్ ను ఉపయోగించాల్సి వస్తే, మీరు `React.SyntheticEvent` టైప్ ను ఉపయోగించవచ్చు, ఇది అన్ని ఈవెంట్స్ కోసం బేస్ టైప్.

### చైల్డ్ ఎలిమెంట్ {/*typing-children*/}

ఒక కాంపోనెంట్ యొక్క చైల్డ్ ఎలిమెంట్ ను వివరించడానికి రెండు సాధారణ మార్గాలు ఉన్నాయి. మొదటిది `React.ReactNode` టైప్ ను ఉపయోగించడం, ఇది JSX లో చైల్డ్ ఎలిమెంట్ గా పంపబడగల అన్ని పోసిబుల్ టైప్ల యొక్క యూనియన్:

```ts
interface ModalRendererProps {
  title: string;
  children: React.ReactNode;
}
```

ఇది చైల్డ్ ఎలిమెంట్ యొక్క బ్రాడ్ డెఫినిషన్. రెండవది `React.ReactElement` టైప్ ను ఉపయోగించడం, ఇది కేవలం JSX ఎలెమెంట్స్ మాత్రమే, JavaScript primitives వంటి strings లేదా numbers కాదు:

```ts
interface ModalRendererProps {
  title: string;
  children: React.ReactElement;
}
```

గమనించండి, మీరు TypeScript ను చైల్డ్ ఎలిమెంట్ ఒక నిర్దిష్ట టైప్ JSX ఎలిమెంట్స్ ని వివరించడానికి ఉపయోగించలేరు, కాబట్టి కేవలం `<li>` చైల్డ్ ఎలిమెంట్ మాత్రమే అంగీకరించే ఒక కంపోనెంట్ ను టైప్-సిస్టమ్‌ ద్వారా వివరించలేరు.

`React.ReactNode` మరియు `React.ReactElement` రెండింటి ఉదాహరణను టైప్-చెక్కర్ తో సహా [ఈ TypeScript ప్లేగ్రౌండ్](https://www.typescriptlang.org/play?#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgIilQ3wChSB6CxYmAOmXRgDkIATJOdNJMGAZzgwAFpxAR+8YADswAVwGkZMJFEzpOjDKw4AFHGEEBvUnDhphwADZsi0gFw0mDWjqQBuUgF9yaCNMlENzgAXjgACjADfkctFnYkfQhDAEpQgD44AB42YAA3dKMo5P46C2tbJGkvLIpcgt9-QLi3AEEwMFCItJDMrPTTbIQ3dKywdIB5aU4kKyQQKpha8drhhIGzLLWODbNs3b3s8YAxKBQAcwXpAThMaGWDvbH0gFloGbmrgQfBzYpd1YjQZbEYARkB6zMwO2SHSAAlZlYIBCdtCRkZpHIrFYahQYQD8UYYFA5EhcfjyGYqHAXnJAsIUHlOOUbHYhMIIHJzsI0Qk4P9SLUBuRqXEXEwAKKfRZcNA8PiCfxWACecAAUgBlAAacFm80W-CU11U6h4TgwUv11yShjgJjMLMqDnN9Dilq+nh8pD8AXgCHdMrCkWisVoAet0R6fXqhWKhjKllZVVxMcavpd4Zg7U6Qaj+2hmdG4zeRF10uu-Aeq0LBfLMEe-V+T2L7zLVu+FBWLdLeq+lc7DYFf39deFVOotMCACNOCh1dq219a+30uC8YWoZsRyuEdjkevR8uvoVMdjyTWt4WiSSydXD4NqZP4AymeZE072ZzuUeZQKheQgA) లో చూడవచ్చు.

### స్టైల్ props {/*typing-style-props*/}

React లో ఇన్లైన్ స్టైల్స్ ఉపయోగిస్తున్నప్పుడు, `style` prop కు పంపబడే ఆబ్జెక్ట్ ను డిస్క్రైబ్ చేయడానికి మీరు `React.CSSProperties` ను ఉపయోగించవచ్చు. ఈ టైప్ అన్ని పాసిబుల్ CSS ప్రాపర్టీస్ యొక్క యూనియన్, మరియు ఇది మీరు `style` prop కు సరైన CSS ప్రాపర్టీస్ పంపిస్తున్నారని నిర్ధారించడానికి మరియు మీ ఎడిటర్ లో ఆటో-కంప్లీట్ పొందడానికి మంచి మార్గం.

```ts
interface MyComponentProps {
  style: React.CSSProperties;
}
```

## మరింత నేర్చుకోవడానికి రిసోర్సెస్ {/*further-learning*/}

ఈ గైడ్ React తో TypeScript ఉపయోగించడం గురించి బేసిక్స్ ను కవర్ చేసింది, కానీ ఇంకా నేర్చుకోవడానికి చాలా ఉంది.
డాక్స్ లోని ఇండివిడ్యుఅల్ API పేజీలలో TypeScript తో వాటిని ఎలా ఉపయోగించాలి అనే దాని గురించి మరింత ఇన్-డెప్త్ డాక్యుమెంటేషన్ కలిగి ఉండవచ్చు.

మేము ఈ కింది రిసోర్సెస్ ను సిఫార్సు చేస్తున్నాము:

 - [TypeScript హ్యాండ్‌బుక్](https://www.typescriptlang.org/docs/handbook/) TypeScript కోసం ఆఫిసిఅల్ డాక్యుమెంటేషన్, మరియు అధిక భాగం కీలక లాంగ్వేజ్ ఫీచర్లను కవర్ చేస్తుంది.

 - [TypeScript రిలీజ్ నోట్స్](https://devblogs.microsoft.com/typescript/) కొత్త ఫీచర్లను ఇన్-డెప్త్ గా కవర్ చేస్తాయి.

 - [React TypeScript చీట్ షీట్](https://react-typescript-cheatsheet.netlify.app/) TypeScript తో React ఉపయోగించడానికి కమ్యూనిటీ-మైన్టైన్డ్ చీట్ షీట్, చాలా ఉపయోగకరమైన ఎడ్జ్ కేసులను కవర్ చేస్తూ ఈ డాక్యుమెంట్ కంటే మరింత విస్తృత తనాన్ని అందిస్తుంది.

 - [TypeScript కమ్యూనిటీ Discord](https://discord.com/invite/typescript) TypeScript మరియు React సమస్యలతో సహాయం కోసం ప్రశ్నలు అడగడానికి మరియు సహాయం పొందడానికి గొప్ప ప్రదేశం.