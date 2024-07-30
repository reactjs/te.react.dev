---
title: TypeScript ని ఉపయోగించడం
re: https://github.com/reactjs/react.dev/issues/5960
---

<Intro>

TypeScript అనేది JavaScript కోడ్‌బేస్‌లకు టైప్ డెఫినిషన్‌లను జోడించడానికి ఒక ప్రసిద్ధ మార్గం. TypeScript [JSX ని సపోర్ట్ చేస్తుంది](/learn/writing-markup-with-jsx) మరియు మీరు మీ ప్రాజెక్ట్‌కి [`@types/react`](https://www.npmjs.com/package/@types/react) మరియు [`@types/react-dom`](https://www.npmjs.com/package/@types/react-dom) ను చేర్చడం ద్వారా పూర్తి React Web సపోర్ట్ని పొందవచ్చు.

</Intro>

<YouWillLearn>

* [React Components తో TypeScript](/learn/typescript#typescript-with-react-components)
* [Hooks తో typing examples](/learn/typescript#example-hooks)
* [`@types/react` నుండి సాధారణ types](/learn/typescript/#useful-types)
* [మరింత తెలుసుకోడానికి స్థానాలు](/learn/typescript/#further-learning)

</YouWillLearn>



## ఇన్‌స్టాలేషన్ {/*installation*/}

అన్ని [production-grade React frameworks](/learn/start-a-new-react-project#production-grade-react-frameworks) TypeScript ఉపయోగాన్ని సపోర్ట్ చేస్తాయి. ఇన్‌స్టాలేషన్ కోసం ఫ్రేమ్‌వర్క్ ప్రత్యేక గైడ్‌ను అనుసరించండి:

- [Next.js](https://nextjs.org/docs/app/building-your-application/configuring/typescript)
- [Remix](https://remix.run/docs/en/1.19.2/guides/typescript)
- [Gatsby](https://www.gatsbyjs.com/docs/how-to/custom-configuration/typescript/)
- [Expo](https://docs.expo.dev/guides/typescript/)
### ఉన్న React ప్రాజెక్ట్‌కు TypeScript ను చేర్చడం {/*adding-typescript-to-an-existing-react-project*/}

React యొక్క type నిర్వచనాల తాజా వెర్షన్ ఇన్‌స్టాల్ చేయడానికి:

<TerminalBlock>
npm install @types/react @types/react-dom
</TerminalBlock>

మీ `tsconfig.json` లో, క్రింది compiler ఆప్షన్స్ సెట్ చేయాలి:

1. [`lib`](https://www.typescriptlang.org/tsconfig/#lib) లో `dom` ఉండాలి (గమనిక: ఎలాంటి `lib` ఆప్షన్ స్పెసిఫ్య్ చేయలేదు అంటే, `dom` డిఫాల్ట్ గా ఉంటుంది).
1. [`jsx`](https://www.typescriptlang.org/tsconfig/#jsx) ని తప్పనిసరిగా వెలిడ్ అయ్యే ఆప్షన్లలో ఒకదానికి సెట్ చేయాలి. చాలా అప్లికేషన్స్‌కి `preserve` సరిపోతుంది.
  మీరు లైబ్రరీని పబ్లిష్ చేస్తున్నట్లు అయితే, ఎలాంటి వేల్యూ ను ఎంచుకోవాలో తెలుసుకోవడానికి [`jsx` డాక్యుమెంటేషన్](https://www.typescriptlang.org/tsconfig/#jsx) ను సంప్రదించండి.

## TypeScript లో React కాంపోనెంట్లను ఎలా రాయడం {/*typescript-with-react-components*/}

<Note>

JSX కలిగి ఉన్న ప్రతి ఫైల్ `.tsx` ఫైల్ విస్తరణను ఉపయోగించాలి. ఇది TypeScript-extension, ఈ ఫైల్ లో JSX ఉందని TypeScript కి తెలియజేస్తుంది.

</Note>

React తో TypeScript వ్రాయడం, React తో JavaScript వ్రాయడముతో చాలా సమానం. ఒక కాంపోనెంట్‌తో పని చేస్తున్నప్పుడు ముఖ్యమైన తేడా మీరు మీ కాంపోనెంట్ యొక్క props కోసం types అందించవచ్చు. ఈ types సరిగ్గా ఉన్నాయో లేదో చెక్ చేయడానికి మరియు editor లో inline documentation అందించడానికి ఉపయోగించవచ్చు.

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
      <h1>Welcome to my app</h1>
      <MyButton title="I'm a button" />
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

ఈ sandboxes TypeScript code ను handle చేయగలవు, కానీ type-checker ను run చేయలేవు. అంటే, మీరు TypeScript sandboxes లో సవరణలు చేయవచ్చు, కానీ మీకు ఏదైనా type errors లేదా హెచ్చరికలు రావు. type-checking పొందడానికి, మీరు [TypeScript Playground](https://www.typescriptlang.org/play) ను లేదా మరింత సర్వసన్నద్ధమైన online sandbox ను ఉపయోగించవచ్చు.

</Note>

ఈ inline syntax ఒక కాంపోనెంట్‌కు types అందించడానికి అత్యంత సులభమైన మార్గం, కానీ మీరు కొన్ని ఫీల్డ్స్‌ను వివరిస్తూ ప్రారంభించినప్పుడు ఇది గందరగోళంగా మారవచ్చు. దీనికి బదులుగా, మీరు కాంపోనెంట్ యొక్క props ను వివరిచేందుకు `interface` లేదా `type` ఉపయోగించవచ్చు:


<Sandpack>

```tsx src/App.tsx active
interface MyButtonProps {
  /** The text to display inside the button */
  title: string;
  /** Whether the button can be interacted with */
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
      <h1>Welcome to my app</h1>
      <MyButton title="I'm a disabled button" disabled={true}/>
    </div>
  );
}
```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```

</Sandpack>

మీ కాంపోనెంట్ యొక్క props ను వివరిస్తున్న type అవసరమున్నంత సులభంగా లేదా క్లిష్టంగా ఉండవచ్చు, కానీ అవి `type` లేదా `interface` తో వివరిస్తే ఒక object type గా ఉండాలి. TypeScript objects ను ఎలా వివరిస్తుందో మీరు [Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html) లో నేర్చుకోవచ్చు కానీ మీరు [Union Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types) ను కూడా props వివరిస్తూ ఉపయోగించడం గురించి ఆసక్తి చూపవచ్చు, ఇది కొన్ని విభిన్న type లలో ఒకటి కావచ్చు మరియు మరింత ఆధునిక ఉపయోగకేసులకు [Creating Types from Types](https://www.typescriptlang.org/docs/handbook/2/types-from-types.html) గైడ్ ఉపయోగపడుతుంది.

## Hooks తో టైప్ ఉదాహరణలు {/*example-hooks*/}

`@types/react` నుండి టైప్ డెఫినిషన్‌లు బిల్ట్-ఇన్ Hooks కోసం టైప్లను కలిగి ఉంటాయి, కాబట్టి మీరు వాటిని ఎలాంటి అదనపు సెటప్ లేకుండానే మీ కాంపోనెంట్లలో ఉపయోగించవచ్చు. అవి మీ కాంపోనెంట్ లో మీరు వ్రాసే కోడ్ ను పరిగణనలోకి తీసుకుంటాయి, కాబట్టి చాలా సార్లు మీరు [ఇన్ఫెరెడ్ టైప్స్](https://www.typescriptlang.org/docs/handbook/type-inference.html) పొందుతారు మరియు సాధారణంగా టైప్స్ ను ఇవ్వడానికి ఎటువంటి సమస్యలు ఎదుర్కొనవలసిన అవసరం లేదు.

అయితే, Hooks కోసం టైప్స్ ను ఎలా అందించాలో కొన్ని ఉదాహరణలను చూద్దాం.

### `useState` {/*typing-usestate*/}

[`useState` Hook](/reference/react/useState) ఇనీషియల్ state గా ఇవ్వబడిన వేల్యూ ను రీ-యూజ్ చేసుకొని ఆ వేల్యూ యొక్క టైప్ ఏమిటి అని నిర్ధారిస్తుంది. ఉదాహరణకు:

```ts
// టైప్ని "boolean" గా సూచిస్తుంది
const [enabled, setEnabled] = useState(false);
```

ఇది `enabled` కు `boolean` టైప్ ను అసైన్ చేస్తుంది, మరియు `setEnabled` `boolean` ఆర్గుమెంట్ ను స్వీకరించే ఫంక్షన్ లేదా `boolean` ను రిటర్న్ చేసే ఫంక్షన్ అవుతుంది. మీరు state కోసం టైప్ ను ఎక్సప్లిసిట్ గా ఇవ్వాలనుకుంటే, మీరు `useState` కాల్ కు టైప్ ఆర్గుమెంట్ ను ఇవ్వవచ్చు:

```ts 
// టైప్ని "boolean" కి ఎక్సప్లిసిట్ గా సెట్ చేయండి
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
      throw new Error("Unknown action");
  }
}

export default function App() {
  const [state, dispatch] = useReducer(stateReducer, initialState);

  const addFive = () => dispatch({ type: "setCount", value: state.count + 5 });
  const reset = () => dispatch({ type: "reset" });

  return (
    <div>
      <h1>Welcome to my counter</h1>

      <p>Count: {state.count}</p>
      <button onClick={addFive}>Add 5</button>
      <button onClick={reset}>Reset</button>
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
    <ThemeContext.Provider value={theme}>
      <MyComponent />
    </ThemeContext.Provider>
  )
}

function MyComponent() {
  const theme = useGetTheme();

  return (
    <div>
      <p>Current theme: {theme}</p>
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

// This is a simpler example, but you can imagine a more complex object here
type ComplexObject = {
  kind: string
};

// The context is created with `| null` in the type, to accurately reflect the default value.
const Context = createContext<ComplexObject | null>(null);

// The `| null` will be removed via the check in the Hook.
const useGetComplexObject = () => {
  const object = useContext(Context);
  if (!object) { throw new Error("useGetComplexObject must be used within a Provider") }
  return object;
}

export default function MyApp() {
  const object = useMemo(() => ({ kind: "complex" }), []);

  return (
    <Context.Provider value={object}>
      <MyComponent />
    </Context.Provider>
  )
}

function MyComponent() {
  const object = useGetComplexObject();

  return (
    <div>
      <p>Current object: {object.kind}</p>
    </div>
  )
}
```

### `useMemo` {/*typing-usememo*/}

[`useMemo`](/reference/react/useMemo) Hook ఒక ఫంక్షన్ కాల్ నుండి ఒక మేమోరైజ్డ్ వేల్యూ ను సృష్టిస్తుంది/రీ-అక్సెస్ చేస్తుంది, 2వ పారామీటర్‌గా పంపబడిన డిపెండెన్సీలు మారినప్పుడు మాత్రమే ఫంక్షన్ రీ-రన్ అవుతుంది. Hook ను కాల్ చేయడం వలన వచ్చిన రిజల్ట్ అనేది మొదటి పారామీటర్‌ లోని ఫంక్షన్ నుండి రిటర్న్ అయిన వాల్యూ ద్వారా అంచనా వేయబడుతుంది. మీరు మరింత ఎక్స్ప్లిసిట్ గా టైప్ ఆర్గుమెంట్ ను Hook కు ప్రొవైడ్ చేయవచ్చు.

```ts
// The type of visibleTodos is inferred from the return value of filterTodos
const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
```


### `useCallback` {/*typing-usecallback*/}

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
  const [value, setValue] = useState("Change me");

  const handleChange = useCallback<React.ChangeEventHandler<HTMLInputElement>>((event) => {
    setValue(event.currentTarget.value);
  }, [setValue])
  
  return (
    <>
      <input value={value} onChange={handleChange} />
      <p>Value: {value}</p>
    </>
  );
}
```

## ఉపయోగకరమైన టైప్స్ {/*useful-types*/}

`@types/react` ప్యాకేజ్ నుండి చాలా విస్తృతమైన types సెట్ వస్తుంది, React మరియు TypeScript ఎలా పరస్పర చర్యలో ఉంటాయో మీరు సౌకర్యంగా భావించినప్పుడు ఇది చదవడం విలువైనది. మీరు వాటిని [DefinitelyTyped లో React యొక్క ఫోల్డర్ లో](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/react/index.d.ts) కనుగొనవచ్చు. ఇక్కడ మేము కొన్ని సాధారణంగా ఉపయోగించే types ను కవర్ చేస్తాము.
### DOM ఈవెంట్స్ {/*typing-dom-events*/}

React లో DOM ఈవెంట్స్ తో పని చేస్తున్నప్పుడు, ఈవెంట్ యొక్క type ఈవెంట్ హ్యాండ్లర్ నుండి తరచుగా అంచనా వేయబడుతుంది. అయితే, ఒక function ను ఈవెంట్ హ్యాండ్లర్ కు పంపించడానికి extraction చేయాలనుకుంటే, మీరు ఈవెంట్ యొక్క type ను స్పష్టంగా సెట్ చేయాలి.
<Sandpack>

```tsx src/App.tsx active
import { useState } from 'react';

export default function Form() {
  const [value, setValue] = useState("Change me");

  function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
    setValue(event.currentTarget.value);
  }

  return (
    <>
      <input value={value} onChange={handleChange} />
      <p>Value: {value}</p>
    </>
  );
}
```

```js src/App.js hidden
import AppTSX from "./App.tsx";
export default App = AppTSX;
```

</Sandpack>

React types లో చాలా రకాల ఈవెంట్స్ అందుబాటులో ఉన్నాయి - పూర్తి జాబితాను [ఇక్కడ](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/b580df54c0819ec9df62b0835a315dd48b8594a9/types/react/index.d.ts#L1247C1-L1373) చూడవచ్చు, ఇది [DOM నుండి ప్రసిద్ధమైన ఈవెంట్స్](https://developer.mozilla.org/en-US/docs/Web/Events) పై ఆధారపడి ఉంటుంది.

మీరు అవసరమైన type ను నిర్ణయిస్తున్నప్పుడు, మీరు ఉపయోగిస్తున్న ఈవెంట్ హ్యాండ్లర్ కోసం హోవర్ సమాచారాన్ని మొదట చూడవచ్చు, ఇది ఈవెంట్ యొక్క type ను చూపిస్తుంది.

ఈ జాబితాలో లేని ఈవెంట్ ను ఉపయోగించాల్సి వస్తే, మీరు `React.SyntheticEvent` type ను ఉపయోగించవచ్చు, ఇది అన్ని ఈవెంట్స్ కోసం బేస్ type.

### Children {/*typing-children*/}

ఒక కంపోనెంట్ యొక్క children ను వివరించడానికి రెండు సాధారణ మార్గాలు ఉన్నాయి. మొదటిది `React.ReactNode` type ను ఉపయోగించడం, ఇది JSX లో children గా పంపబడగల అన్ని సంభావ్య type ల యొక్క యూనియన్:

```ts
interface ModalRendererProps {
  title: string;
  children: React.ReactNode;
}
```

ఇది children యొక్క విస్తృత నిర్వచనం. రెండవది `React.ReactElement` type ను ఉపయోగించడం, ఇది కేవలం JSX elements మాత్రమే, JavaScript primitives వంటి strings లేదా numbers కాదు:

```ts
interface ModalRendererProps {
  title: string;
  children: React.ReactElement;
}
```

గమనించండి, మీరు TypeScript ను children ఒక నిర్దిష్ట రకం JSX elements అని వివరించడానికి ఉపయోగించలేరు, కాబట్టి కేవలం `<li>` children మాత్రమే అంగీకరించే ఒక కంపోనెంట్ ను type-system ద్వారా వివరించలేరు.

`React.ReactNode` మరియు `React.ReactElement` రెండింటి ఉదాహరణను type-checker తో సహా [ఈ TypeScript playground](https://www.typescriptlang.org/play?#code/JYWwDg9gTgLgBAJQKYEMDG8BmUIjgIilQ3wChSB6CxYmAOmXRgDkIATJOdNJMGAZzgwAFpxAR+8YADswAVwGkZMJFEzpOjDKw4AFHGEEBvUnDhphwADZsi0gFw0mDWjqQBuUgF9yaCNMlENzgAXjgACjADfkctFnYkfQhDAEpQgD44AB42YAA3dKMo5P46C2tbJGkvLIpcgt9-QLi3AEEwMFCItJDMrPTTbIQ3dKywdIB5aU4kKyQQKpha8drhhIGzLLWODbNs3b3s8YAxKBQAcwXpAThMaGWDvbH0gFloGbmrgQfBzYpd1YjQZbEYARkB6zMwO2SHSAAlZlYIBCdtCRkZpHIrFYahQYQD8UYYFA5EhcfjyGYqHAXnJAsIUHlOOUbHYhMIIHJzsI0Qk4P9SLUBuRqXEXEwAKKfRZcNA8PiCfxWACecAAUgBlAAacFm80W-CU11U6h4TgwUv11yShjgJjMLMqDnN9Dilq+nh8pD8AXgCHdMrCkWisVoAet0R6fXqhWKhjKllZVVxMcavpd4Zg7U6Qaj+2hmdG4zeRF10uu-Aeq0LBfLMEe-V+T2L7zLVu+FBWLdLeq+lc7DYFf39deFVOotMCACNOCh1dq219a+30uC8YWoZsRyuEdjkevR8uvoVMdjyTWt4WiSSydXD4NqZP4AymeZE072ZzuUeZQKheQgA) లో చూడవచ్చు.

### Style Props {/*typing-style-props*/}

React లో inline styles ఉపయోగిస్తున్నప్పుడు, `style` prop కు పంపబడే object ను వర్ణించడానికి మీరు `React.CSSProperties` ను ఉపయోగించవచ్చు. ఈ type అన్ని సంభావ్య CSS properties యొక్క యూనియన్, మరియు ఇది మీరు `style` prop కు సరైన CSS properties పంపిస్తున్నారని నిర్ధారించడానికి మరియు మీ ఎడిటర్ లో auto-complete పొందడానికి మంచి మార్గం.

```ts
interface MyComponentProps {
  style: React.CSSProperties;
}
```

## మరింత నేర్చుకోవడానికి {/*further-learning*/}

ఈ గైడ్ React తో TypeScript ఉపయోగించడం గురించి ప్రాథమికాలను కవర్ చేసింది, కానీ ఇంకా నేర్చుకోవడానికి చాలా ఉంది.
Docs లోని వ్యక్తిగత API పేజీలు TypeScript తో వాటిని ఎలా ఉపయోగించాలో గురించి మరింత లోతైన డాక్యుమెంటేషన్ కలిగి ఉండవచ్చు.

మేము ఈ కింది రిసోర్సెస్ ను సిఫార్సు చేస్తున్నాము:

 - [TypeScript హ్యాండ్‌బుక్](https://www.typescriptlang.org/docs/handbook/) TypeScript కోసం ఆఫిసిఅల్ డాక్యుమెంటేషన్, మరియు అధిక భాగం కీలక లాంగ్వేజ్ ఫీచర్లను కవర్ చేస్తుంది.

 - [The TypeScript release notes](https://devblogs.microsoft.com/typescript/) కొత్త లక్షణాలను లోతుగా కవర్ చేస్తాయి.

 - [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/) TypeScript తో React ఉపయోగించడానికి కమ్యూనిటీ-నిర్వహిత చీట్ షీట్, చాలా ఉపయోగకరమైన ఎడ్జ్ కేసులను కవర్ చేస్తూ ఈ డాక్యుమెంట్ కంటే మరింత విస్తృతతనాన్ని అందిస్తుంది.

 - [TypeScript Community Discord](https://discord.com/invite/typescript) TypeScript మరియు React సమస్యలతో సహాయం కోసం ప్రశ్నలు అడగడానికి మరియు సహాయం పొందడానికి గొప్ప ప్రదేశం.