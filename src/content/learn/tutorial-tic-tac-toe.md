---
title: 'ట్యుటోరియల్: టిక్-టాక్-టో'
---

<Intro>

ఈ ట్యుటోరియల్ లో మీరు ఒక చిన్న టిక్-టాక్-టో గేమ్ ని బిల్డ్ చేస్తారు. ఈ ట్యుటోరియల్ మీకు ఎలాంటి React ఫ్రేమ్ వర్క్ పరిజ్ఞానం లేదని భావిస్తుంది. ఈ ట్యుటోరియల్ లో మీరు నేర్చుకునే టెక్నిక్స్ ఏవైనా React యాప్ ని బిల్డ్ చేయడానికి ఫండమెంటల్గా ఉంటాయి, మరియు దానిని పూర్తిగా అర్థం చేసుకోవడం వల్ల React గురించి మీకు లోతైన అవగాహన లభిస్తుంది.

</Intro>

<Note>

ఈ ట్యుటోరియల్ **చేయడం ద్వారా నేర్చుకోవడానికి** ఇష్టపడే వారికి మరియు త్వరగా ఏదైనా సృష్టించాలనుకునే వ్యక్తుల కోసం రూపొందించబడింది. మీరు ప్రతి కాన్సెప్ట్ ని స్టెప్ బై స్టెప్ గా నేర్చుకోవాలనుకుంటే, [UI ని వివరించడం](/learn/describing-the-ui) ద్వారా ప్రారంభించండి.

</Note>

ఈ ట్యుటోరియల్ అనేక విభాగాలుగా విభజించబడింది:

- [ట్యుటోరియల్ కోసం సెటప్](#setup-for-the-tutorial) మీరు ట్యుటోరియల్‌ని అనుసరించడానికి **స్టార్టింగ్ పాయింట్** ని అందిస్తుంది.
- [ఒవెర్వ్యూ](#overview) మీకు React యొక్క **ఫండమెంటల్స్** ను నేర్పుతుంది: కంపోనెంట్స్, props మరియు state.
- [గేమ్‌ను పూర్తి చేయడం](#completing-the-game) మీకు React డెవలప్‌మెంట్‌లో వాడే **అత్యంత సాధారణ టెక్నిక్‌లను** నేర్పుతుంది.
- [టైం ట్రావెల్ ని జోడించడం](#adding-time-travel) వలన React యొక్క ప్రత్యేక బలాలపై మీకు **లోతైన అంతర్దృష్టి** లభిస్తుంది.

### మీరు ఏమి నిర్మించబోతున్నారు? {/*what-are-you-building*/}

ఈ ట్యుటోరియల్‌లో, మీరు React ‌తో ఇంటరాక్టివ్ టిక్-టాక్-టో గేమ్‌ని నిర్మిస్తారు.

మీరు పూర్తి చేసినప్పుడు అది ఎలా ఉంటుందో మీరు ఇక్కడ చూడవచ్చు:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const xIsNext = currentMove % 2 === 0;
  const currentSquares = history[currentMove];

  function handlePlay(nextSquares) {
    const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
    setHistory(nextHistory);
    setCurrentMove(nextHistory.length - 1);
  }

  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li key={move}>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

మీకు ఇంకా కోడ్ అర్థం కాకపోయినా లేదా ఈ కోడ్ యొక్క సింటాక్స్ గురించి తెలియకపోయినా, చింతించకండి! ఈ ట్యుటోరియల్ యొక్క లక్ష్యం React మరియు దాని సింటాక్స్‌ను అర్థం చేసుకోవడంలో మీకు సహాయం చేయడం.

ట్యుటోరియల్‌తో కొనసాగడానికి ముందు మీరు పైన ఉన్న టిక్-టాక్-టో గేమ్‌ని తనిఖీ చేయాలని మేము సిఫార్సు చేస్తున్నాము. మీరు గమనించే ఫీచర్లలో ఒకటి గేమ్ బోర్డ్ యొక్క కుడి వైపున సంఖ్యా జాబితా ఉంది. ఈ జాబితా మీకు గేమ్‌లో జరిగిన అన్ని కదలికల చరిత్రను అందిస్తుంది మరియు గేమ్ అభివృద్ధి చెందుతున్నప్పుడు ఇది అప్డేట్ అవుతుంది.

మీరు పూర్తి చేసిన టిక్-టాక్-టో గేమ్‌ని ఆడిన తర్వాత, పేజీని స్క్రోల్ చేస్తూ ఉండండి. ఈ ట్యుటోరియల్ సింప్లెర్ టెంప్లేట్‌తో ప్రారంభమవుతుంది. తదుపరి దశ మీ గేమ్‌ను సెటప్ చేయడం, తద్వారా మీరు దీన్ని సృష్టించడం ప్రారంభించవచ్చు.

## ట్యుటోరియల్ కోసం సెటప్ {/*setup-for-the-tutorial*/}

దిగువ లైవ్ కోడ్ ఎడిటర్‌లో, CodeSandbox వెబ్‌సైట్‌ని ఉపయోగించి కొత్త ట్యాబ్‌లో ఎడిటర్‌ను తెరవడానికి టాప్-రైట్ కార్నర్లో ఉన్న **Fork** ని క్లిక్ చేయండి. CodeSandbox మీ బ్రౌజర్‌లో కోడ్‌ను వ్రాయడానికి మరియు మీరు సృష్టించిన యాప్‌ని మీ యూజర్స్ ఎలా చూస్తారనే ప్రివ్యూని అందిస్తుంది. కొత్త ట్యాబ్‌లో ఈ ట్యుటోరియల్ కోసం ఖాళీ స్క్వేర్ మరియు స్టార్టర్ కోడ్‌ను చూస్తారు.

<Sandpack>

```js src/App.js
export default function Square() {
  return <button className="square">X</button>;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

<Note>

మీరు మీ లోకల్ డెవలప్మెంట్ ఎన్విరాన్మెంట్ ని ఉపయోగించి కూడా ఈ ట్యుటోరియల్‌ని అనుసరించవచ్చు. దీన్ని చేయడానికి, మీరు వీటిని చేయాలి:

1. [Node.js](https://nodejs.org/en/) ని ఇన్‌స్టాల్ చేయండి
1. మీరు ఇంతకు ముందు ఓపెన్ చేసిన CodeSandbox ట్యాబ్‌లో, మెనుని తెరవడానికి టాప్-లెఫ్ట్ కార్నర్ లో ఉన్న బటన్ను క్లిక్ చేయండి, ఆపై ఫైల్‌ల ఆర్కైవ్‌ను లోకల్ గా డౌన్‌లోడ్ చేయడానికి ఆ మెనులో **Download Sandbox** ని క్లిక్ చేయండి
1. ఆర్కైవ్‌ను అన్జిప్ చేసి, ఆపై మీరు అన్జిప్ చేసిన డైరెక్టరీని టెర్మినల్ లో `cd` ని ఉపయోగించి తెరవండి
1. `npm install` తో డిపెండెన్సీలను ఇన్‌స్టాల్ చేయండి
1. లోకల్ సర్వర్‌ని స్టార్ట్ చేయడానికి `npm start` ని రన్ చేయండి మరియు బ్రౌజర్‌లో రన్ అవుతున్న కోడ్‌ను వీక్షించడానికి ప్రాంప్ట్‌లను అనుసరించండి

మీరు ఎక్కడైనా ఆగిపోయినట్లైతే, నిరుత్సాహపడకండి! దయచేసి ఆన్‌లైన్‌లో కొనసాగండి మరియు మీ లోకల్ ఎన్విరాన్మెంట్ని తర్వాత మళ్లీ సెటప్ చేయడానికి ప్రయత్నించండి.

</Note>

## ఒవెర్వ్యూ {/*overview*/}

సెటప్ పూర్తయింది కాబట్టి, ఇప్పుడు React యొక్క ఒవెర్వ్యూ ని చూద్దాం!

### స్టార్టర్ కోడ్‌ని ఇంస్పెక్ట్ చేయడం {/*inspecting-the-starter-code*/}

CodeSandbox లో మీరు మూడు ప్రధాన విభాగాలను చూస్తారు:

![CodeSandbox స్టార్టర్ కోడ్](../images/tutorial/react-starter-code-codesandbox.png)

1. `App.js`, `index.js`, `styles.css` వంటి ఫైల్‌ల జాబితా మరియు `public` అనే ఫోల్డర్‌తో _Files_ విభాగం
1. _కోడ్ ఎడిటర్_ ఇక్కడ మీరు ఎంచుకున్న ఫైల్ యొక్క సోర్స్ కోడ్‌ని మీరు చూస్తారు
1. మీరు వ్రాసిన కోడ్ ఎలా ప్రదర్శించబడుతుందో మీరు చూసే _browser_ విభాగం

`App.js` ఫైల్ ని ఇప్పుడు _Files_ విభాగంలో సెలెక్ట్ చేయండి. _కోడ్ ఎడిటర్_ లో ఫైల్ యొక్క కంటెంట్‌ ఇలా ఉండాలి:

```jsx
export default function Square() {
  return <button className="square">X</button>;
}
```

_బ్రౌసర్_ విభాగం ఇలా X తో కూడిన స్క్వేర్ ని ప్రదర్శించాలి:

![X నిండిన స్క్వేర్](../images/tutorial/x-filled-square.png)

ఇప్పుడు స్టార్టర్ కోడ్‌లోని ఫైల్‌లను చూద్దాం.

#### `App.js` {/*appjs*/}

`App.js` లోని కోడ్ _కాంపోనెంట్_ ని క్రియేట్ చేస్తుంది. React లో, ఒక కాంపోనెంట్ అనేది UI లో కొంత భాగాన్ని రిప్రజెంట్ చేసే రీయూజబుల్ కోడ్ యొక్క భాగం. మీ అప్లికేషన్‌లోని UI ఎలిమెంట్‌లను రెండర్ చేయడానికి, మేనేజ్ చేయడానికి మరియు అప్‌డేట్ చేయడానికి కాంపోనెంట్లు ఉపయోగించబడతాయి. కాంపోనెంట్ లో లైన్ బై లైన్ గా ఏం జరుగుతుందో చూద్దాం:

```js {1}
export default function Square() {
  return <button className="square">X</button>;
}
```

మొదటి లైన్ `Square` అనే ఫంక్షన్‌ని డిఫైన్ చేస్తుంది. `export` JavaScript కీవర్డ్ ఈ ఫంక్షన్‌ని ఈ ఫైల్ బయట నుండి యాక్సెస్ చేయడానికి సహాయపడుతుంది. `default` కీవర్డ్ మీ కోడ్‌ని ఉపయోగించే ఇతర ఫైల్‌లకు ఇదే మీ ఫైల్‌లోని మెయిన్ ఫంక్షన్ అని చెబుతుంది.

```js {2}
export default function Square() {
  return <button className="square">X</button>;
}
```

రెండవ లైన్ బటన్‌ను అందిస్తుంది. `return` JavaScript కీవర్డ్ అంటే ఆ తర్వాత వచ్చేది ఫంక్షన్ కాలర్‌కు వేల్యూ గా అందించబడుతుంది. `<button>` అనేది *JSX ఎలిమెంట్*. JSX ఎలిమెంట్ అనేది JavaScript కోడ్ మరియు HTML ట్యాగ్‌ల కలయిక, ఇది మీరు ఏమి ప్రదర్శించాలనుకుంటున్నారో వివరిస్తుంది. `className="square"` అనేది బటన్ ప్రాపర్టీ లేదా *props* ఇది బటన్‌ను ఎలా స్టైల్ చేయాలో CSS కి తెలియజేస్తుంది. `X` అనేది బటన్ లోపల ప్రదర్శించబడే టెక్స్ట్ మరియు `</button>` కింది కంటెంట్‌ బటన్ లోపల ఉంచకూడదని సూచించడానికి JSX ఎలిమెంట్ ని మూసివేస్తుంది.

#### `styles.css` {/*stylescss*/}

CodeSandbox యొక్క _Files_ విభాగంలో `styles.css` అని లేబుల్ చేయబడిన ఫైల్‌పై క్లిక్ చేయండి. ఈ ఫైల్ మీ React యాప్ కోసం స్టైల్‌లను డిఫైన్ చేస్తుంది. మొదటి రెండు _CSS సెలెక్టర్‌లు_ (`*` మరియు `body`) మీ యాప్‌లోని పెద్ద భాగాల స్టైల్ ని డిఫైన్ చేస్తాయి, అయితే `.square` సెలెక్టర్ `className` ప్రాపర్టీని `square` కి సెట్ చేసిన ఏదైనా కాంపోనెంట్ యొక్క స్టైల్‌ ని డిఫైన్ చేస్తుంది. మీ కోడ్‌లో, అది `App.js` ఫైల్‌లోని మీ Square కాంపోనెంట్ నుండి బటన్‌తో మ్యాచ్ అవుతుంది.

#### `index.js` {/*indexjs*/}

CodeSandbox యొక్క _Files_ విభాగంలో `index.js` అని లేబుల్ చేయబడిన ఫైల్‌పై క్లిక్ చేయండి. మీరు ట్యుటోరియల్ సమయంలో ఈ ఫైల్‌ని ఎడిట్ చేయరు కానీ మీరు `App.js` ఫైల్‌లో క్రియేట్ చేసిన కాంపోనెంట్ మరియు వెబ్ బ్రౌజర్‌కి మధ్య ఇది వంతెన లా పని చేస్తుంది.

```jsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import './styles.css';

import App from './App';
```

1-5 లైన్స్ అవసరమైన అన్ని ముక్కలను ఒకచోట చేర్చాయి: 

* React
* వెబ్ బ్రౌజర్‌లతో మాట్లాడటానికి React లైబ్రరీ (React DOM)
* మీ కాంపోనెంట్ల కోసం స్టైల్స్
* మీరు `App.js` లో క్రియేట్ చేసిన కాంపోనెంట్.

ఫైల్‌లోని మిగిలిన భాగం అన్ని ముక్కలను ఒకచోట చేర్చి, ఫైనల్ ప్రోడక్ట్ ని `public` ఫోల్డర్‌లోని `index.html` కి ఇంజెక్ట్ చేస్తుంది.

### బోర్డును నిర్మించడం {/*building-the-board*/}

మళ్లీ `App.js` కి వెళ్దాం. మీరు మిగిలిన ట్యుటోరియల్‌ని ఇక్కడే స్పెండ్ చేస్తారు.

ప్రస్తుత బోర్డులో ఒక్క స్క్వేర్ మాత్రమే ఉంది, కానీ వాస్తవానికి మీకు తొమ్మిది అవసరం! మీరు రెండవ స్క్వేర్ ని సృష్టించడానికి కాపీ చేసి పేస్ట్ చేస్తే...

```js {2}
export default function Square() {
  return <button className="square">X</button><button className="square">X</button>;
}
```

మీకు ఈ ఎర్రర్ వస్తుంది:

<ConsoleBlock level="error">

/src/App.js: Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX Fragment `<>...</>`?

</ConsoleBlock>

React కాంపోనెంట్‌లు ఈ బటన్ లాగా ఒకదానికొకటి పక్కన ఉన్న మల్టిపుల్ JSX ఎలిమెంట్‌లు కాకుండా ఒక్క JSX ఎలిమెంట్‌ని మాత్రమే రిటర్న్ చేయాలి. దీన్ని పరిష్కరించడానికి మీరు ఇలా ప్రక్కనే ఉన్న అనేక JSX ఎలిమెంట్లను చుట్టడానికి *ఫ్రాగ్మెంట్స్* (`<>` మరియు `</>`) ను ఉపయోగించవచ్చు:

```js {3-6}
export default function Square() {
  return (
    <>
      <button className="square">X</button>
      <button className="square">X</button>
    </>
  );
}
```

మీరు ఈ ఔట్పుట్ ని చూస్తారు:

![రెండు X నిండిన స్క్వేర్స్](../images/tutorial/two-x-filled-squares.png)

గ్రేట్! మీరు చేయాల్సిందల్లా తొమ్మిది స్క్వేర్లు ఉండే వరకు కొన్ని సార్లు కాపీ చేసి పేస్ట్ చేయండి...

![ఒక లైన్ లో తొమ్మిది X నిండిన స్క్వేర్స్](../images/tutorial/nine-x-filled-squares.png)

అరెరే! స్క్వేర్లు అన్నీ ఒకే లైన్ లో ఉన్నాయి, మన బోర్డు కోసం మీకు అవసరమైన గ్రిడ్‌లో కాదు. దీన్ని పరిష్కరించడానికి మీరు మీ స్క్వేర్‌లను `div` లతో వరుసలుగా (rows) గ్రూప్ చేయాలి మరియు కొన్ని CSS క్లాస్లను జోడించాలి. మీరు దాని వద్ద ఉన్నప్పుడు, ప్రతి స్క్వేర్ ఎక్కడ ప్రదర్శించబడుతుందో మీకు తెలుసని నిర్ధారించుకోవడానికి మీరు ప్రతి స్క్వేర్‌కు ఒక సంఖ్యను ఇస్తారు.

`App.js` ఫైల్‌లో, ఇలా కనిపించేలా `Square` కాంపోనెంట్‌ని అప్‌డేట్ చేయండి:

```js {3-19}
export default function Square() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}
```

`styles.css` లో డిఫైన్ చేయబడిన CSS, `board-row` యొక్క `className` తో divs ని స్టైల్ చేస్తుంది. ఇప్పుడు మీరు మీ కాంపోనెంట్‌లను స్టైల్ చేసిన `div` లతో వరుసలుగా గ్రూప్ చేసారు కాబట్టి మీరు మీ టిక్-టాక్-టో బోర్డుని కలిగి ఉన్నారు:

![టిక్-టాక్-టో బోర్డు 1 నుండి 9 వరకు సంఖ్యలతో నిండి ఉంటుంది](../images/tutorial/number-filled-board.png)

అయితే మరో సమస్య వచ్చింది. దీనిని `Square` కాంపోనెంట్ అని పిలిచినప్పటికీ, ఇది వాస్తవానికి ఇకపై స్క్వేర్ కాదు. దీన్ని పరిష్కరించడానికి, పేరును `Board` గా మార్చండి:

```js {1}
export default function Board() {
  //...
}
```

ఈ దశలో, మీ కోడ్ ఇలా ఉండాలి:

<Sandpack>

```js
export default function Board() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

<Note>

అయ్యో, టైప్ చేయడానికి ఇది చాలా ఎక్కువ! ఈ పేజీ నుండి కోడ్‌ని కాపీ చేసి పేస్ట్ చేయడం సరైంది కాదు. అయితే, మీరు ఒక చిన్న సవాలు కోసం సిద్ధంగా ఉన్నట్లయితే, మీరు మాన్యువల్‌గా కనీసం ఒక్కసారైనా టైప్ చేసిన కోడ్‌ను మాత్రమే కాపీ చేయమని మేము సిఫార్సు చేస్తున్నాము.

</Note>

### props ద్వారా డేటాను పంపడం {/*passing-data-through-props*/}

తర్వాత, యూసర్ స్క్వేర్‌ పై క్లిక్ చేసినప్పుడు మీరు స్క్వేర్ వేల్యూ ను ఖాళీ నుండి "X" కి మార్చాలనుకుంటున్నారు. మీరు ఇప్పటివరకు బోర్డ్‌ను ఎలా నిర్మించారు అనే దానితో మీరు స్క్వేర్‌ను తొమ్మిది సార్లు అప్‌డేట్ చేసే కోడ్‌ను కాపీ-పేస్ట్ చేయాలి (మీ వద్ద ఉన్న ప్రతి స్క్వేర్‌కు ఒకసారి)! కాపీ-పేస్ట్ చేయడానికి బదులుగా, మీరు రీయూజబుల్ కాంపోనెంట్లను సృష్టించడానికి మరియు డూప్లికేట్‌లతో నిండిన చిందరవందరగా ఉన్న కోడ్‌ను వ్రాయకుండా నిరోధించడానికి React యొక్క కాంపోనెంట్ ఆర్కిటెక్చర్‌ని ఉపయోగించవచ్చు.

ముందుగా, మీరు మీ `Board` కాంపోనెంట్ నుండి మీ మొదటి స్క్వేర్ (`<button className="square">1</button>`) ని డిఫైన్ చేసే లైన్ ని కొత్త `Square` కాంపోనెంట్‌కి కాపీ చేయబోతున్నారు:

```js {1-3}
function Square() {
  return <button className="square">1</button>;
}

export default function Board() {
  // ...
}
```

JSX సింటాక్స్‌ని ఉపయోగించి ఆ `Square` కాంపోనెంట్‌ని రెండర్ చేయడానికి మీరు `Board` కాంపోనెంట్‌ని అప్‌డేట్ చేస్తారు:

```js {5-19}
// ...
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

బ్రౌజర్ `div` ల మాదిరిగా కాకుండా, మీరు సృష్టించే కాంపోనెంట్లు `Board` మరియు `Square` తప్పనిసరిగా క్యాపిటల్ లెటర్ తో స్టార్ట్ అవ్వాలి.

ఏమి జరిగిందో చూద్దాం:

![1 తో నిండిన పూర్తి బోర్డు](../images/tutorial/board-filled-with-ones.png)

అరెరే! మీరు ఇంతకు ముందు ఉన్న సంఖ్యా స్క్వేర్లను కోల్పోయారు. ఇప్పుడు ప్రతి స్క్వేర్ "1" అని చెబుతుంది. దీన్ని పరిష్కరించడానికి, మీరు ప్రతి స్క్వేర్ కలిగి ఉండవలసిన వేల్యూ ను పేరెంట్ కాంపోనెంట్ (`Board`) నుండి దాని చైల్డ్ (`Square`) కి పాస్ చేయడానికి *props* ని ఉపయోగిస్తారు.

మీరు `Board` నుండి పాస్ చేసే `value` ప్రాప్‌ని రీడ్ చేయడానికి `Square` కాంపోనెంట్‌ను అప్‌డేట్ చేయండి:

```js {1}
function Square({ value }) {
  return <button className="square">1</button>;
}
```

`function Square({ value })` అనేది స్క్వేర్ కాంపోనెంట్‌ను `value` అనే ప్రాప్‌ని పాస్ చేయవచ్చని సూచిస్తుంది.

ఇప్పుడు మీరు ప్రతి స్క్వేర్ లోపల `1` కి బదులుగా ఆ `value` ని ప్రదర్శించాలనుకుంటున్నారు. ఈ విధంగా చేయడానికి ప్రయత్నించండి:

```js {2}
function Square({ value }) {
  return <button className="square">value</button>;
}
```

అయ్యో, ఇది మీరు అనుకున్న అవుట్పుట్ కాదు:

!["value" నిండిన బోర్డు](../images/tutorial/board-filled-with-value.png)

మీరు మీ కాంపోనెంట్ నుండి `value` అనే JavaScript వేరియబుల్‌ని రెండర్ చేయాలనుకుంటున్నారు, "value" పదం కాదు. JSX నుండి "JavaScript లోకి ఎస్కేప్ అవ్వడానికి", మీకు కర్లీ బ్రేస్‌లు అవసరం. JSX లో `value` చుట్టూ కర్లీ బ్రేస్‌లను ఇలా జోడించండి:

```js {2}
function Square({ value }) {
  return <button className="square">{value}</button>;
}
```

ప్రస్తుతానికి, మీరు ఖాళీ బోర్డుని చూడాలి:

![ఖాళీ బోర్డు](../images/tutorial/empty-board.png)

ఎందుకంటే, `Board` కాంపోనెంట్ అది రెండర్ చేసే ప్రతి `Square` కాంపోనెంట్‌కి `value` ప్రాప్‌ను ఇంకా పాస్ చేయలేదు. దాన్ని పరిష్కరించడానికి మీరు `Board` కాంపోనెంట్ ద్వారా రెండర్ చేయబడిన ప్రతి `Square` కాంపోనెంట్‌కి `value` ప్రాప్‌ని జోడిస్తారు:

```js {5-7,10-12,15-17}
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>
      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>
      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}
```

ఇప్పుడు మీరు మళ్లీ సంఖ్యల గ్రిడ్‌ని చూడాలి:

![టిక్-టాక్-టో బోర్డు 1 నుండి 9 వరకు సంఖ్యలతో నిండి ఉంటుంది](../images/tutorial/number-filled-board.png)

మీ అప్డేటెడ్ కోడ్ ఇలా ఉండాలి:

<Sandpack>

```js src/App.js
function Square({ value }) {
  return <button className="square">{value}</button>;
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>
      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>
      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

### ఇంటరాక్టివ్ కాంపోనెంట్ ని తయారు చేయడం {/*making-an-interactive-component*/}

మీరు క్లిక్ చేసినప్పుడు `Square` కాంపోనెంట్‌ను `X` తో నింపండి. `Square` లోపల `handleClick` అనే ఫంక్షన్‌ను డిక్లేర్ చేయండి. ఆపై, `Square` నుండి రిటర్న్ అయిన బటన్ JSX ఎలిమెంట్ యొక్క ప్రాప్‌లకు `onClick` ని జోడించండి:

```js {2-4,9}
function Square({ value }) {
  function handleClick() {
    console.log('clicked!');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}
```

మీరు ఇప్పుడు స్క్వేర్‌పై క్లిక్ చేస్తే, CodeSandbox లోని _Browser_ విభాగం దిగువన ఉన్న _Console_ ట్యాబ్‌లో `"clicked!"` అని చెప్పే లాగ్ మీకు కనిపిస్తుంది. స్క్వేర్‌ని ఒకటి కంటే ఎక్కువసార్లు క్లిక్ చేయడం వలన `"clicked!"` మళ్లీ లాగ్ అవుతుంది. ఒకే మెసేజ్ తో రిపీట్ అయ్యే కన్సోల్ లాగ్‌లు కన్సోల్‌లో మరిన్ని లైన్‌లను సృష్టించవు. బదులుగా, మీరు మీ మొదటి `"clicked!"` లాగ్ పక్కన ఇంక్రిమెంటింగ్ కౌంటర్‌ని చూస్తారు.

<Note>

మీరు మీ లోకల్ డెవలప్మెంట్ ఎన్విరాన్మెంట్ ని ఉపయోగించి ఈ ట్యుటోరియల్‌ని అనుసరిస్తుంటే, మీరు మీ బ్రౌజర్ కన్సోల్‌ను తెరవాలి. ఉదాహరణకు, మీరు Chrome బ్రౌజర్‌ని ఉపయోగిస్తుంటే, మీరు కన్సోల్‌ను కీబోర్డ్ షార్ట్‌కట్‌తో **Shift + Ctrl + J** (Windows/Linux లో) లేదా **Option + ⌘ + J** (macOS లో) వీక్షించవచ్చు.

</Note>

తదుపరి దశగా, మీరు `Square` కాంపోనెంట్ అది క్లిక్ చేయబడిందని "గుర్తుంచుకోవాలి" మరియు దానిని "X" గుర్తుతో నింపాలని మీరు కోరుకుంటారు. విషయాలను "గుర్తుంచుకోవడానికి", కాంపోనెంట్లు *state* ని ఉపయోగిస్తాయి.

React అనేది `useState` అనే ప్రత్యేక ఫంక్షన్‌ని అందిస్తుంది, మీరు దాన్ని మీ కాంపోనెంట్ నుండి కాల్ చేయడం ద్వారా ఇది విషయాలను "గుర్తుపెట్టుకొంటుంది". `Square` కరెంట్ వేల్యూ ను state లో స్టోర్ చేసి, `Square` క్లిక్ చేసినప్పుడు దాన్ని మారుద్దాం.

ఫైల్ టాప్ లో `useState` ని ఇంపోర్ట్ చేయండి. `Square` కాంపోనెంట్ నుండి `value` ప్రాప్‌ను రిమూవ్ చేయండి. బదులుగా, `Square` ప్రారంభానికి కొత్త లైన్ ని జోడించి, `useState` ని కాల్ చేయండి. `value` అనే state వేరియబుల్ రిటర్న్ అయింది అని ఇది నిర్ధారిస్తుంది.

```js {1,3,4}
import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    //...
```

`value` state యొక్క కరెంట్ వేల్యూ ని స్టోర్ చేస్తుంది మరియు `setValue` అనేది ఆ వేల్యూ ను అప్డేట్ చేయడానికి ఉపయోగించే ఫంక్షన్. `useState` కి పంపబడిన `null` వేల్యూ ఈ state వేరియబుల్‌కు ఇనీటియాల్ వేల్యూ గా ఉపయోగించబడుతుంది, కాబట్టి `value` అనేది `null` వేల్యూ తో ప్రారంభమవుతుంది.

`Square` కాంపోనెంట్ ఇకపై props ను యాక్సెప్ట్ చేయడు కాబట్టి, మీరు `Board` కాంపోనెంట్ సృష్టించిన మొత్తం తొమ్మిది స్క్వేర్ కాంపోనెంట్ల నుండి `value` ప్రాప్‌ను రిమూవ్ చేస్తారు:

```js {6-8,11-13,16-18}
// ...
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

ఇప్పుడు మీరు క్లిక్ చేసినప్పుడు "X" ని ప్రదర్శించడానికి `Square` ని మారుస్తారు. `console.log("clicked!");` ఈవెంట్ హ్యాండ్లర్‌ను `setValue('X');` తో రీప్లేస్ చేయండి. ఇప్పుడు మీ `Square` కాంపోనెంట్ ఇలా కనిపిస్తుంది:

```js {5}
function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    setValue('X');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}
```

`onClick` హ్యాండ్లర్ నుండి ఈ `set` ఫంక్షన్‌ ని కాల్ చేయడం ద్వారా, మీరు దాని `<button>` ని క్లిక్ చేసినప్పుడల్లా ఆ `Square` ని రీ-రెండర్ చేయమని React కి చెబుతున్నారు. అప్డేట్ తర్వాత, `Square` యొక్క `value` `'X'` అవుతుంది, కాబట్టి మీరు గేమ్ బోర్డ్‌లో "X" ని చూస్తారు. ఏదైనా స్క్వేర్‌పై క్లిక్ చేయండి మరియు "X" ని చూడండి:

![బోర్డ్‌కు మల్టిపుల్ "X" లని జోడించండి](../images/tutorial/tictac-adding-x-s.gif)

ప్రతి స్క్వేర్ దాని స్వంత state ని కలిగి ఉంటుంది: ప్రతి స్క్వేర్‌లో స్టోర్ చేయబడిన `value` ఇతర వాటితో సంబంధం లేకుండా ఉంటుంది. మీరు కాంపోనెంట్‌లో `set` ఫంక్షన్‌ ని కాల్ చేసినప్పుడు, React ఆటోమేటిక్‌గా లోపల ఉన్న చైల్డ్ కాంపోనెంట్‌లను కూడా అప్‌డేట్ చేస్తుంది.

మీరు పైన చెప్పిన మార్పులు చేసిన తర్వాత, మీ కోడ్ ఇలా కనిపిస్తుంది:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square() {
  const [value, setValue] = useState(null);

  function handleClick() {
    setValue('X');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}

export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

### React Developer Tools {/*react-developer-tools*/}

React DevTools మీ React కాంపోనెంట్‌ల props మరియు state ని చెక్ చేయడానికి మిమ్మల్ని అనుమతిస్తాయి. CodeSandbox లోని _Browser_ విభాగం దిగువన మీరు React DevTools ట్యాబ్‌ను కనుగొనవచ్చు:

![CodeSandbox లోని React DevTools](../images/tutorial/codesandbox-devtools.png)

స్క్రీన్‌పై పర్టికులర్ కాంపోనెంట్ ని ఇన్స్పెక్ట చేయడానికి, React DevTools టాప్ లెఫ్ట్ కార్నర్లో ఉన్న బటన్‌ను ఉపయోగించండి:

![React DevTools తో పేజీలోని కాంపోనెంట్లను సెలెక్ట్ చేయడం](../images/tutorial/devtools-select.gif)

<Note>

లోకల్ డెవలప్మెంట్ కోసం, React DevTools [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en), [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/), మరియు [Edge](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil) బ్రౌజర్ ఎక్స్టెన్షన్ గా అందుబాటులో ఉంది. దీన్ని ఇన్‌స్టాల్ చేయండి మరియు React ని ఉపయోగించే సైట్‌ల కోసం మీ బ్రౌజర్ డెవలపర్ టూల్స్‌లో *Components* ట్యాబ్ కనిపిస్తుంది.

</Note>

## గేమ్‌ను పూర్తి చేయడం {/*completing-the-game*/}

ఈ సమయానికి, మీరు మీ టిక్-టాక్-టో గేమ్ కోసం అన్ని బేసిక్ బిల్డింగ్ బ్లాక్‌లను కలిగి ఉన్నారు. పూర్తి గేమ్‌ను కలిగి ఉండటానికి, మీరు ఇప్పుడు "X"లు మరియు "O"లను బోర్డ్‌లో ఆల్టర్నేట్గా ఉంచాలి మరియు విజేతను నిర్ణయించడానికి మీకు ఒక మార్గం అవసరం.

### state ని లిఫ్ట్ చేయడం {/*lifting-state-up*/}

ప్రస్తుతం, ప్రతి `Square` కాంపోనెంట్ గేమ్ state లో కొంత భాగాన్ని నిర్వహిస్తోంది. టిక్-టాక్-టో గేమ్‌లో విజేత ఎవరో చెక్ చేయడానికి, `Board` లోని 9 `Square` కాంపోనెంట్‌లలోని ప్రతి state ని తెలుసుకోవాలి.

మీరు దానిని ఎలా చేరుకుంటారు? మొదట, మీరు `Board` ప్రతి `Square` ని ఆ `Square` state కోసం "అడగాలి" అని ఊహించవచ్చు. React లో ఈ విధానం టెక్నికల్గా సాధ్యమే అయినప్పటికీ, కోడ్ అర్థం చేసుకోవడం కష్టంగా మారడం, బగ్‌లకు గురికావడం మరియు రీఫ్యాక్టర్ చేయడం కష్టం కాబట్టి మేము దానిని సిఫార్సు చెయ్యట్లేదు. బదులుగా, ప్రతి `Square` లో కాకుండా పేరెంట్ `Board` కాంపోనెంట్‌లో గేమ్ state ని స్టోర్ చేయడం ఉత్తమ విధానం. మీరు ప్రతి స్క్వేర్‌కి ఒక నంబర్‌ను పాస్ చేసినప్పుడు, props ను పాస్ చేయడం ద్వారా ప్రతి `Square` కి ఏమి ప్రదర్శించాలో `Board` కాంపోనెంట్ తెలియజేస్తుంది.

**మల్టిపుల్ చైల్డ్ల నుండి డేటాను సేకరించడానికి లేదా ఇద్దరు చైల్డ్ కాంపోనెంట్లు ఒకదానితో ఒకటి కమ్యూనికేట్ చేయడానికి, వారి పేరెంట్ కాంపోనెంట్‌లో షేర్డ్ state ని డిక్లేర్ చేయండి. పేరెంట్ కాంపోనెంట్ ఆ state ని props ద్వారా చైల్డ్లకు తిరిగి పంపగలదు. ఇది చైల్డ్ కాంపోనెంట్లు ఒకదానితో ఒకటి మరియు వారి పేరెంట్ తో సింక్ (sync) లో ఉండేలా చేస్తుంది.**

React కాంపోనెంట్‌లు రీఫ్యాక్టరేట్ చేయబడినప్పుడు state ని పేరెంట్ కాంపోనెంట్‌కి లిఫ్ట్ చేయడం సాధారణం.

దీనిని ప్రయత్నిద్దాం. `Board` కాంపోనెంట్‌ని ఎడిట్ చేయండి, తద్వారా ఇది 9 స్క్వేర్‌లకు కరెస్పాండింగ్ గా 9 null ల array కి డిఫాల్ట్‌గా ఉండే `squares` అనే state వేరియబుల్‌ను డిక్లేర్ చేస్తుంది:

```js {3}
// ...
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    // ...
  );
}
```

`Array(9).fill(null)` తొమ్మిది ఎలెమెంట్లతో ఒక array ని క్రియేట్ చేస్తుంది మరియు వాటిలో ప్రతి ఒక్కటి `null` కి సెట్ చేస్తుంది. దాని చుట్టూ ఉన్న `useState()` కాల్ ప్రారంభంలో ఆ array కి సెట్ చేయబడిన `squares` state వేరియబుల్‌ని డిక్లేర్ చేస్తుంది. array లోని ప్రతి ఎంట్రీ స్క్వేర్ వేల్యూ కు అనుగుణంగా ఉంటుంది. మీరు తర్వాత బోర్డ్‌ను ఫిల్ చేసినప్పుడు, `squares` array ఇలా కనిపిస్తుంది:

```jsx
['O', null, 'X', 'X', 'X', 'O', 'O', null, null]
```

ఇప్పుడు మీ `Board` కాంపోనెంట్ అది రెండర్ చేసే ప్రతి `Square` కి `value` props ని పాస్ చేయాలి:

```js {6-8,11-13,16-18}
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} />
        <Square value={squares[1]} />
        <Square value={squares[2]} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} />
        <Square value={squares[4]} />
        <Square value={squares[5]} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} />
        <Square value={squares[7]} />
        <Square value={squares[8]} />
      </div>
    </>
  );
}
```

తర్వాత, మీరు `Board` కాంపోనెంట్ నుండి `value` ప్రాప్‌ను స్వీకరించడానికి `Square` కాంపోనెంట్‌ని ఎడిట్ చేస్తారు. దీనికి స్క్వేర్ కాంపోనెంట్ యొక్క సొంత స్టేట్‌ఫుల్ ట్రాకింగ్ `value` మరియు బటన్ యొక్క `onClick` ప్రాప్‌ని తీసివేయడం అవసరం:

```js {1,2}
function Square({value}) {
  return <button className="square">{value}</button>;
}
```

ఈ సమయంలో మీరు ఖాళీ టిక్-టాక్-టో బోర్డుని చూడాలి:

![ఖాళీ బోర్డు](../images/tutorial/empty-board.png)

మరియు మీ కోడ్ ఇలా ఉండాలి:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value }) {
  return <button className="square">{value}</button>;
}

export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} />
        <Square value={squares[1]} />
        <Square value={squares[2]} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} />
        <Square value={squares[4]} />
        <Square value={squares[5]} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} />
        <Square value={squares[7]} />
        <Square value={squares[8]} />
      </div>
    </>
  );
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

ప్రతి స్క్వేర్ ఇప్పుడు `value` ప్రాప్‌ని అందుకుంటుంది, అది `'X'`, `'O'` లేదా ఖాళీ స్క్వేర్‌ల కోసం `null`.

తర్వాత, మీరు `Square` ని క్లిక్ చేసినప్పుడు ఏమి జరుగుతుందో మార్చాలి. `Board` కాంపోనెంట్ ఇప్పుడు ఏ స్క్వేర్‌లను ఫిల్ చేయాలో మైంటైన్ చేస్తుంది. మీరు `Board` state ని అప్డేట్ చేయడానికి `Square` కోసం ఒక మార్గాన్ని సృష్టించాలి. state దానిని డిఫైన్ చేసే కాంపోనెంట్కి ప్రైవేట్‌గా ఉన్నందున, మీరు `Square` నుండి డైరెక్ట్గా `Board` state ని అప్డేట్ చేయలేరు.

బదులుగా, మీరు `Board` కాంపోనెంట్ నుండి `Square` కాంపోనెంట్‌కి ఒక ఫంక్షన్‌ను పాస్ చేస్తారు మరియు మీరు స్క్వేర్ ని క్లిక్ చేసినప్పుడు `Square` ఆ ఫంక్షన్‌ని కాల్ చేస్తుంది. మీరు క్లిక్ చేసినప్పుడు `Square` కాంపోనెంట్ కాల్ చేసే ఫంక్షన్‌తో ప్రారంభిస్తారు. మీరు ఆ ఫంక్షన్‌ని `onSquareClick` అని పిలుస్తారు:

```js {3}
function Square({ value }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}
```

తర్వాత, మీరు `onSquareClick` ఫంక్షన్‌ని `Square` కాంపోనెంట్ యొక్క props కు జోడిస్తారు:

```js {1}
function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}
```

ఇప్పుడు మీరు `onSquareClick` ప్రాప్‌ని `Board` కాంపోనెంట్‌లోని ఫంక్షన్‌కి కనెక్ట్ చేస్తారు, దానికి మీరు `handleClick` అని పేరు పెట్టారు. `onSquareClick` ని `handleClick` కి కనెక్ట్ చేయడానికి, మీరు మొదటి `Square` కాంపోనెంట్ యొక్క `onSquareClick` ప్రాప్‌కి ఒక ఫంక్షన్‌ని పాస్ చేస్తారు:

```js {7}
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={handleClick} />
        //...
  );
}
```

చివరగా, మీరు మీ బోర్డు state ని కలిగి ఉన్న `squares` array ని అప్డేట్ చేయడానికి `Board` కాంపోనెంట్ లోపల `handleClick` ఫంక్షన్‌ని డిఫైన్ చేస్తారు:

```js {4-8}
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick() {
    const nextSquares = squares.slice();
    nextSquares[0] = "X";
    setSquares(nextSquares);
  }

  return (
    // ...
  )
}
```

`handleClick` ఫంక్షన్ JavaScript `slice()` array మెథొద్స్ (methods) ని ఉపయోగించి `squares` array (`nextSquares`) యొక్క కాపీని క్రియేట్ చేస్తుంది. ఆపై, మొదటి (`[0]` ఇండెక్స్) స్క్వేర్‌కి `X` ని జోడించడానికి `handleClick` `nextSquares` array ని అప్డేట్ చేస్తుంది.

`setSquares` ఫంక్షన్‌ని కాల్ చేయడం వలన కాంపోనెంట్ యొక్క state మారిందని React తెలుసుకోవచ్చు. ఇది `squares` state (`Board`) అలాగే దాని చైల్డ్ కాంపోనెంట్‌లను (బోర్డ్‌ను రూపొందించే `Square` కాంపోనెంట్లు) ఉపయోగించే కాంపోనెంట్‌ల రీ-రెండర్‌ను ట్రిగ్గర్ చేస్తుంది.

<Note>

JavaScript [క్లోసురేష్స్ (closures)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) ని సపోర్ట్ చేస్తుంది అంటే ఇన్నర్ ఫంక్షన్కు (ఉదా. `handleClick`) ఔటర్ ఫంక్షన్‌లో డిఫైన్ చేయబడిన వేరియబుల్స్ మరియు ఫంక్షన్‌లకు యాక్సెస్‌ను కలిగి ఉంటుంది (ఉదా. `Board`). `handleClick` ఫంక్షన్ `squares` state ని రీడ్ చేయగలదు మరియు `setSquares` మెథడ్ ని కాల్ చేయగలదు ఎందుకంటే అవి రెండూ `Board` ఫంక్షన్‌లో డిఫైన్ చేయబడ్డాయి.

</Note>

ఇప్పుడు మీరు X లను బోర్డ్‌కి జోడించవచ్చు... కానీ అప్పర్ లెఫ్ట్ స్క్వేర్కి మాత్రమే. అప్పర్ లెఫ్ట్ స్క్వేర్ (`0`) కోసం ఇండెక్స్ ను అప్డేట్ చేయడానికి మీ `handleClick` ఫంక్షన్ హార్డ్‌కోడ్ చేయబడింది. ఏదైనా స్క్వేర్‌ని అప్‌డేట్ చేయడానికి `handleClick` ని అప్‌డేట్ చేద్దాం. అప్‌డేట్ చేయడానికి స్క్వేర్ ఇండెక్స్‌ను తీసుకునే `handleClick` ఫంక్షన్‌కు ఆర్గ్యుమెంట్ `i` ని జోడించండి:

```js {4,6}
export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    const nextSquares = squares.slice();
    nextSquares[i] = "X";
    setSquares(nextSquares);
  }

  return (
    // ...
  )
}
```

తర్వాత, మీరు ఆ `i` ని `handleClick` కి పాస్ చేయాలి. మీరు స్క్వేర్ యొక్క `onSquareClick` ప్రాప్‌ని నేరుగా JSX లో `handleClick(0)` గా సెట్ చేయడానికి ప్రయత్నించవచ్చు, కానీ అది పని చేయదు:

```jsx
<Square value={squares[0]} onSquareClick={handleClick(0)} />
```

ఇది ఎందుకు పని చేయలేదని ఇక్కడ ఉంది. `handleClick(0)` కాల్ Board కాంపోనెంట్‌ను రెండరింగ్ చేయడంలో భాగంగా ఉంటుంది. `setSquares` ని కాల్ చేయడం ద్వారా `handleClick(0)` Board కాంపోనెంట్ యొక్క state ని మారుస్తుంది కాబట్టి, మీ మొత్తం Board కాంపోనెంట్ మళ్లీ రెండర్ చేయబడుతుంది. కానీ ఇది మళ్లీ `handleClick(0)` ని రన్ చేస్తుంది, ఇది ఇన్ఫైనైట్ లూప్‌కు దారి తీస్తుంది:

<ConsoleBlock level="error">

Too many re-renders. React limits the number of renders to prevent an infinite loop.

</ConsoleBlock>

ఇంతకు ముందు ఈ సమస్య ఎందుకు రాలేదు?

మీరు `onSquareClick={handleClick}` ని పాస్ చేస్తున్నప్పుడు, మీరు `handleClick` ఫంక్షన్‌ను props గా పాస్ చేస్తున్నారు. అప్పుడు మీరు దానిని కాల్ చేయలేదు! కానీ ఇప్పుడు మీరు ఆ ఫంక్షన్‌ ని వెంటనే *కాల్* చేస్తున్నారు - `handleClick(0)` లో పారేన్తేసెస్ ని గమనించండి--అందుకే ఇది చాలా త్వరగా రన్ అవుతుంది. యూసర్ క్లిక్ చేసే వరకు మీరు `handleClick` ని కాల్ చేయకూడదు!

మీరు `handleClick(0)` ని కాల్ చేసే `handleFirstSquareClick`, `handleClick(1)` ని కాల్ చేసే `handleSecondSquareClick` వంటి ఫంక్షన్‌ని క్రియేట్ చేయడం ద్వారా దీన్ని పరిష్కరించవచ్చు. మీరు ఈ ఫంక్షన్‌లను `onSquareClick={handleFirstSquareClick}` వంటి props గా (కాల్ చేయకుండా) పాస్ చేస్తారు. ఇది ఇన్ఫైనైట్ లూప్‌ను సాల్వ్ చేస్తుంది.

అయితే, తొమ్మిది వేర్వేరు ఫంక్షన్లను డిఫైన్ చేయడం మరియు వాటిలో ప్రతిదానికి పేరు ఇవ్వడం చాలా కష్టం. బదులుగా, ఇలా చేద్దాం:

```js {6}
export default function Board() {
  // ...
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        // ...
  );
}
```

కొత్త `() =>` సింటాక్స్‌ని గమనించండి. ఇక్కడ, `() => handleClick(0)` అనేది *ఆర్రౌ ఫంక్షన్*, ఇది ఫంక్షన్‌లను డిఫైన్ చేయడానికి ఒక చిన్న మార్గం. స్క్వేర్ ని క్లిక్ చేసినప్పుడు, `=>` "ఆర్రౌ" తర్వాత ఉన్న కోడ్ రన్ చేయబడుతుంది, `handleClick(0)` ని కాల్ చేస్తుంది.

మీరు పాస్ చేసే ఆర్రౌ ఫంక్షన్‌ల నుండి `handleClick` ని కాల్ చేయడానికి ఇప్పుడు మీరు ఇతర ఎనిమిది స్క్వేర్‌లను అప్‌డేట్ చేయాలి. `handleClick` యొక్క ప్రతి కాల్‌కు సంబంధించిన ఆర్గ్యుమెంట్ సరైన స్క్వేర్ యొక్క ఇండెక్స్కు అనుగుణంగా ఉందని నిర్ధారించుకోండి:

```js {6-8,11-13,16-18}
export default function Board() {
  // ...
  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
};
```

ఇప్పుడు మీరు వాటిపై క్లిక్ చేయడం ద్వారా బోర్డ్‌లోని ఏదైనా స్క్వేర్‌కి మళ్లీ X లను జోడించవచ్చు:

![X తో బోర్డు నింపడం](../images/tutorial/tictac-adding-x-s.gif)

కానీ ఈసారి state మేనేజ్మెంట్ అంతా `Board` కాంపోనెంట్ దే!

మీ కోడ్ ఇలా ఉండాలి:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

export default function Board() {
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    const nextSquares = squares.slice();
    nextSquares[i] = 'X';
    setSquares(nextSquares);
  }

  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

ఇప్పుడు మీ state హ్యాండ్లింగ్ `Board` కాంపోనెంట్‌లో ఉంది, పేరెంట్ `Board` కాంపోనెంట్ చైల్డ్ `Square` కాంపోనెంట్‌లకు props ను పంపుతుంది, తద్వారా అవి సరిగ్గా ప్రదర్శించబడతాయి. `Square` పై క్లిక్ చేసినప్పుడు, చైల్డ్ `Square` కాంపోనెంట్ ఇప్పుడు బోర్డ్ state ని అప్‌డేట్ చేయమని పేరెంట్ `Board` కాంపోనెంట్‌ని అడుగుతుంది. `Board` యొక్క state మారినప్పుడు, `Board` కాంపోనెంట్ మరియు ప్రతి చైల్డ్ `Square` కాంపోనెంట్లు ఆటోమెటికల్గా రీ-రెండర్ అవుతాయి. అన్ని స్క్వేర్‌ల state ని `Board` కాంపోనెంట్‌లో ఉంచడం వల్ల భవిష్యత్తులో విజేతను గుర్తించడానికి ఇది అనుమతిస్తుంది.

యూసర్ మీ బోర్డ్‌లో `X` ని జోడించడానికి టాప్ లెఫ్ట్ స్క్వేర్‌ను క్లిక్ చేసినప్పుడు ఏమి జరుగుతుందో మళ్ళీ చూద్దాం:

1. టాప్ లెఫ్ట్ స్క్వేర్‌పై క్లిక్ చేయడం ద్వారా `button` దాని `Square` నుండి `onClick` ప్రాప్‌గా స్వీకరించిన ఫంక్షన్‌ను రన్ చేస్తుంది. `Square` కాంపోనెంట్ ఆ ఫంక్షన్‌ను `Board` నుండి దాని `onSquareClick` ప్రాప్‌గా స్వీకరించింది. `Board` కాంపోనెంట్ ఆ ఫంక్షన్‌ని నేరుగా JSX లో డిఫైన్ చేసింది. ఇది `0` ఆర్గ్యుమెంట్‌తో `handleClick` ని కాల్ చేస్తుంది.
1. `squares` array లోని మొదటి ఎలిమెంట్ ని `null` నుండి `X` కి అప్డేట్ చేయడానికి `handleClick` ఆర్గ్యుమెంట్ (`0`) ని ఉపయోగిస్తుంది.
1. `Board` కాంపోనెంట్ యొక్క `squares` state అప్డేట్ చేయబడింది, కాబట్టి `Board` మరియు దాని చైల్డ్స్ అందరూ మళ్ళీ రెండర్ అవుతారు. ఇది `0` ఇండెక్స్తో ఉన్న `Square` కాంపోనెంట్ యొక్క `value` ప్రాప్‌ను `null` నుండి `X` కి మార్చడానికి కారణమవుతుంది.

చివరగా, యూసర్ టాప్ లెఫ్ట్ స్క్వేర్‌ని క్లిక్ చేసిన తర్వాత అది ఖాళీ నుండి `X` గా మారడం చూస్తారు.

<Note>

DOM `<button>` ఎలిమెంట్ యొక్క `onClick` అట్రిబ్యూట్ React కి ప్రత్యేక అర్ధాన్ని కలిగి ఉంది ఎందుకంటే ఇది బిల్ట్-ఇన్ కాంపోనెంట్. `Square` వంటి కస్టమ్ కాంపోనెంట్ల కోసం, పేరు పెట్టడం మీ ఇష్టం. మీరు `Square` యొక్క `onSquareClick` ప్రాప్ లేదా `Board` యొక్క `handleClick` ఫంక్షన్ కి ఏదైనా పేరు పెట్టవచ్చు మరియు కోడ్ అదే పని చేస్తుంది. React ‌లో, ఈవెంట్‌లను రెప్రెసెంత్ చేసే props కోసం `onSomething` పేర్లను ఉపయోగించడం మరియు ఆ ఈవెంట్‌లను హేండిల్ చేసే ఫంక్షన్ డెఫినిషన్‌ల కోసం `handleSomething` ని ఉపయోగించడం సంప్రదాయం.

</Note>

### ఎందుకు ఇమ్ముటబిలిటీ ముఖ్యం {/*why-immutability-is-important*/}

ఇప్పటికే ఉన్న array ని అప్డేట్ చేయడానికి బదులుగా `squares` array యొక్క కాపీని సృష్టించడానికి `handleClick` లో మీరు `.slice()` అని ఎలా కాల్ చేస్తారో గమనించండి. ఎందుకు అని వివరించడానికి, మనం ఇమ్ముటబిలిటీ గురించి చర్చించాలి మరియు ఇమ్ముటబిలిటీ ఎందుకు ముఖ్యమో నేర్చుకోవాలి.

డేటాను మార్చడానికి సాధారణంగా రెండు విధానాలు ఉన్నాయి. డేటా వేల్యూ ను నేరుగా మార్చడం ద్వారా డేటాను _మ్యుటేట్_ చేయడం మొదటి విధానం. కావలసిన మార్పులను కలిగి ఉన్న కొత్త కాపీతో డేటాను రీప్లేస్ చేయడం రెండవ విధానం. మీరు `squares` array ని మ్యుటేట్ చేసినట్లయితే అది ఎలా ఉంటుందో ఇక్కడ ఉంది:

```jsx
const squares = [null, null, null, null, null, null, null, null, null];
squares[0] = 'X';
// Now `squares` is ["X", null, null, null, null, null, null, null, null];
```

మీరు `squares` array ని మ్యుటేట్ చేయకుండా డేటాను చేంజ్ చేసినట్లయితే అది ఎలా ఉంటుందో ఇక్కడ ఉంది:

```jsx
const squares = [null, null, null, null, null, null, null, null, null];
const nextSquares = ['X', null, null, null, null, null, null, null, null];
// Now `squares` is unchanged, but `nextSquares` first element is 'X' rather than `null`
```

ఫలితం ఒకే విధంగా ఉంటుంది కానీ డైరెక్ట్ గా మ్యుటేట్ చేయకుండా ఉండటం (లోపల ఉన్న డేటాను మార్చడం) ద్వారా, మీరు అనేక ప్రయోజనాలను పొందుతారు.

ఇమ్ముటబిలిటీ కాంప్లెక్స్ ఫీచర్లను ఇంప్లిమెంట్ చేయడం చాలా సులభం చేస్తుంది. ఈ ట్యుటోరియల్‌లో తర్వాత, మీరు గేమ్ చరిత్రను రివ్యూ చేయడానికి మరియు గత కదలికలకు "జంప్ బ్యాక్" అవ్వడానికి మిమ్మల్ని అనుమతించే "టైమ్ ట్రావెల్" ఫీచర్‌ను అమలు చేస్తారు. ఈ ఫంక్షనాలిటీ గేమ్‌లకు ప్రత్యేకమైనది కాదు--నిర్దిష్ట చర్యలను అన్డు మరియు రీడు చేయడం అనేది యాప్‌లకు సాధారణ అవసరం. డైరెక్ట్ డేటా మ్యుటేషన్‌ను నివారించడం వలన డేటా యొక్క మునుపటి వెర్షన్‌లను అలాగే ఉంచడానికి మరియు వాటిని తర్వాత మళ్లీ ఉపయోగించుకోవడానికి మిమ్మల్ని అనుమతిస్తుంది.

ఇమ్ముటబిలిటీ వల్ల మరో ప్రయోజనం కూడా ఉంది. డిఫాల్ట్‌గా, పేరెంట్ కాంపోనెంట్ స్థితి మారినప్పుడు అన్ని చైల్డ్ కాంపోనెంట్‌లు ఆటోమేటిక్‌గా రీ-రెండర్ అవుతాయి. మార్పు వల్ల ప్రభావితం కాని చైల్డ్ కాంపోనెంట్‌లు కూడా ఇందులో ఉన్నాయి. రీ-రెండరింగ్ అనేది యూసర్ నోటీస్ చేయనప్పటికీ (మీరు దానిని అవొఇద్ చేయడానికి యాక్టివ్ గా ట్రై చేయకూడదు!), మీరు పెర్ఫార్మన్స్ ఇస్సుఎస్ వల్ల ట్రీ లో క్లియర్గా అఫక్ట్ అవ్వని కొంత భాగాన్ని రీ-రెండరింగ్ చేయడం స్కిప్ చేయవచ్చు. ఇమ్యుటబిలిటీ వారి డేటా మారినదా లేదా అనేదానిని పోల్చడానికి కాంపోనెంట్లను చాలా చౌకగా చేస్తుంది. మీరు [`memo` API రిఫరెన్స్](/reference/react/memo) లో కాంపోనెంట్‌ను ఎప్పుడు రీ-రెండర్ చేయాలో React ఎలా ఎంచుకుంటుంది అనే దాని గురించి మరింత తెలుసుకోవచ్చు.

### Taking turns {/*taking-turns*/}

It's now time to fix a major defect in this tic-tac-toe game: the "O"s cannot be marked on the board.

You'll set the first move to be "X" by default. Let's keep track of this by adding another piece of state to the Board component:

```js {2}
function Board() {
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  // ...
}
```

Each time a player moves, `xIsNext` (a boolean) will be flipped to determine which player goes next and the game's state will be saved. You'll update the `Board`'s `handleClick` function to flip the value of `xIsNext`:

```js {7,8,9,10,11,13}
export default function Board() {
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = "X";
    } else {
      nextSquares[i] = "O";
    }
    setSquares(nextSquares);
    setXIsNext(!xIsNext);
  }

  return (
    //...
  );
}
```

Now, as you click on different squares, they will alternate between `X` and `O`, as they should!

But wait, there's a problem. Try clicking on the same square multiple times:

![O overwriting an X](../images/tutorial/o-replaces-x.gif)

The `X` is overwritten by an `O`! While this would add a very interesting twist to the game, we're going to stick to the original rules for now.

When you mark a square with a `X` or an `O` you aren't first checking to see if the square already has a `X` or `O` value. You can fix this by *returning early*. You'll check to see if the square already has a `X` or an `O`. If the square is already filled, you will `return` in the `handleClick` function early--before it tries to update the board state.

```js {2,3,4}
function handleClick(i) {
  if (squares[i]) {
    return;
  }
  const nextSquares = squares.slice();
  //...
}
```

Now you can only add `X`'s or `O`'s to empty squares! Here is what your code should look like at this point:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({value, onSquareClick}) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

export default function Board() {
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    if (squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    setSquares(nextSquares);
    setXIsNext(!xIsNext);
  }

  return (
    <>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

### Declaring a winner {/*declaring-a-winner*/}

Now that the players can take turns, you'll want to show when the game is won and there are no more turns to make. To do this you'll add a helper function called `calculateWinner` that takes an array of 9 squares, checks for a winner and returns `'X'`, `'O'`, or `null` as appropriate. Don't worry too much about the `calculateWinner` function; it's not specific to React:

```js src/App.js
export default function Board() {
  //...
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

<Note>

It does not matter whether you define `calculateWinner` before or after the `Board`. Let's put it at the end so that you don't have to scroll past it every time you edit your components.

</Note>

You will call `calculateWinner(squares)` in the `Board` component's `handleClick` function to check if a player has won. You can perform this check at the same time you check if a user has clicked a square that already has a `X` or and `O`. We'd like to return early in both cases:

```js {2}
function handleClick(i) {
  if (squares[i] || calculateWinner(squares)) {
    return;
  }
  const nextSquares = squares.slice();
  //...
}
```

To let the players know when the game is over, you can display text such as "Winner: X" or "Winner: O". To do that you'll add a `status` section to the `Board` component. The status will display the winner if the game is over and if the game is ongoing you'll display which player's turn is next:

```js {3-9,13}
export default function Board() {
  // ...
  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = "Winner: " + winner;
  } else {
    status = "Next player: " + (xIsNext ? "X" : "O");
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        // ...
  )
}
```

Congratulations! You now have a working tic-tac-toe game. And you've just learned the basics of React too. So _you_ are the real winner here. Here is what the code should look like:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({value, onSquareClick}) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

export default function Board() {
  const [xIsNext, setXIsNext] = useState(true);
  const [squares, setSquares] = useState(Array(9).fill(null));

  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    setSquares(nextSquares);
    setXIsNext(!xIsNext);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

## Adding time travel {/*adding-time-travel*/}

As a final exercise, let's make it possible to "go back in time" to the previous moves in the game.

### Storing a history of moves {/*storing-a-history-of-moves*/}

If you mutated the `squares` array, implementing time travel would be very difficult.

However, you used `slice()` to create a new copy of the `squares` array after every move, and treated it as immutable. This will allow you to store every past version of the `squares` array, and navigate between the turns that have already happened.

You'll store the past `squares` arrays in another array called `history`, which you'll store as a new state variable. The `history` array represents all board states, from the first to the last move, and has a shape like this:

```jsx
[
  // Before first move
  [null, null, null, null, null, null, null, null, null],
  // After first move
  [null, null, null, null, 'X', null, null, null, null],
  // After second move
  [null, null, null, null, 'X', null, null, null, 'O'],
  // ...
]
```

### Lifting state up, again {/*lifting-state-up-again*/}

You will now write a new top-level component called `Game` to display a list of past moves. That's where you will place the `history` state that contains the entire game history.

Placing the `history` state into the `Game` component will let you remove the `squares` state from its child `Board` component. Just like you "lifted state up" from the `Square` component into the `Board` component, you will now lift it up from the `Board` into the top-level `Game` component. This gives the `Game` component full control over the `Board`'s data and lets it instruct the `Board` to render previous turns from the `history`.

First, add a `Game` component with `export default`. Have it render the `Board` component and some markup:

```js {1,5-16}
function Board() {
  // ...
}

export default function Game() {
  return (
    <div className="game">
      <div className="game-board">
        <Board />
      </div>
      <div className="game-info">
        <ol>{/*TODO*/}</ol>
      </div>
    </div>
  );
}
```

Note that you are removing the `export default` keywords before the `function Board() {` declaration and adding them before the `function Game() {` declaration. This tells your `index.js` file to use the `Game` component as the top-level component instead of your `Board` component. The additional `div`s returned by the `Game` component are making room for the game information you'll add to the board later.

Add some state to the `Game` component to track which player is next and the history of moves:

```js {2-3}
export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  // ...
```

Notice how `[Array(9).fill(null)]` is an array with a single item, which itself is an array of 9 `null`s.

To render the squares for the current move, you'll want to read the last squares array from the `history`. You don't need `useState` for this--you already have enough information to calculate it during rendering:

```js {4}
export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const currentSquares = history[history.length - 1];
  // ...
```

Next, create a `handlePlay` function inside the `Game` component that will be called by the `Board` component to update the game. Pass `xIsNext`, `currentSquares` and `handlePlay` as props to the `Board` component:

```js {6-8,13}
export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const currentSquares = history[history.length - 1];

  function handlePlay(nextSquares) {
    // TODO
  }

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
        //...
  )
}
```

Let's make the `Board` component fully controlled by the props it receives. Change the `Board` component to take three props: `xIsNext`, `squares`, and a new `onPlay` function that `Board` can call with the updated squares array when a player makes a move. Next, remove the first two lines of the `Board` function that call `useState`:

```js {1}
function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    //...
  }
  // ...
}
```

Now replace the `setSquares` and `setXIsNext` calls in `handleClick` in the `Board` component with a single call to your new `onPlay` function so the `Game` component can update the `Board` when the user clicks a square:

```js {12}
function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = "X";
    } else {
      nextSquares[i] = "O";
    }
    onPlay(nextSquares);
  }
  //...
}
```

The `Board` component is fully controlled by the props passed to it by the `Game` component. You need to implement the `handlePlay` function in the `Game` component to get the game working again.

What should `handlePlay` do when called? Remember that Board used to call `setSquares` with an updated array; now it passes the updated `squares` array to `onPlay`.

The `handlePlay` function needs to update `Game`'s state to trigger a re-render, but you don't have a `setSquares` function that you can call any more--you're now using the `history` state variable to store this information. You'll want to update `history` by appending the updated `squares` array as a new history entry. You also want to toggle `xIsNext`, just as Board used to do:

```js {4-5}
export default function Game() {
  //...
  function handlePlay(nextSquares) {
    setHistory([...history, nextSquares]);
    setXIsNext(!xIsNext);
  }
  //...
}
```

Here, `[...history, nextSquares]` creates a new array that contains all the items in `history`, followed by `nextSquares`. (You can read the `...history` [*spread syntax*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) as "enumerate all the items in `history`".)

For example, if `history` is `[[null,null,null], ["X",null,null]]` and `nextSquares` is `["X",null,"O"]`, then the new `[...history, nextSquares]` array will be `[[null,null,null], ["X",null,null], ["X",null,"O"]]`.

At this point, you've moved the state to live in the `Game` component, and the UI should be fully working, just as it was before the refactor. Here is what the code should look like at this point:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const currentSquares = history[history.length - 1];

  function handlePlay(nextSquares) {
    setHistory([...history, nextSquares]);
    setXIsNext(!xIsNext);
  }

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{/*TODO*/}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

### Showing the past moves {/*showing-the-past-moves*/}

Since you are recording the tic-tac-toe game's history, you can now display a list of past moves to the player.

React elements like `<button>` are regular JavaScript objects; you can pass them around in your application. To render multiple items in React, you can use an array of React elements.

You already have an array of `history` moves in state, so now you need to transform it to an array of React elements. In JavaScript, to transform one array into another, you can use the [array `map` method:](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

```jsx
[1, 2, 3].map((x) => x * 2) // [2, 4, 6]
```

You'll use `map` to transform your `history` of moves into React elements representing buttons on the screen, and display a list of buttons to "jump" to past moves. Let's `map` over the `history` in the Game component:

```js {11-13,15-27,35}
export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const currentSquares = history[history.length - 1];

  function handlePlay(nextSquares) {
    setHistory([...history, nextSquares]);
    setXIsNext(!xIsNext);
  }

  function jumpTo(nextMove) {
    // TODO
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}
```

You can see what your code should look like below. Note that you should see an error in the developer tools console that says: 

<ConsoleBlock level="warning">
Warning: Each child in an array or iterator should have a unique "key" prop. Check the render method of &#96;Game&#96;.
</ConsoleBlock>
  
You'll fix this error in the next section.

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const currentSquares = history[history.length - 1];

  function handlePlay(nextSquares) {
    setHistory([...history, nextSquares]);
    setXIsNext(!xIsNext);
  }

  function jumpTo(nextMove) {
    // TODO
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}

.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

As you iterate through `history` array inside the function you passed to `map`, the `squares` argument goes through each element of `history`, and the `move` argument goes through each array index: `0`, `1`, `2`, …. (In most cases, you'd need the actual array elements, but to render a list of moves you will only need indexes.)

For each move in the tic-tac-toe game's history, you create a list item `<li>` which contains a button `<button>`. The button has an `onClick` handler which calls a function called `jumpTo` (that you haven't implemented yet).

For now, you should see a list of the moves that occurred in the game and an error in the developer tools console. Let's discuss what the "key" error means.

### Picking a key {/*picking-a-key*/}

When you render a list, React stores some information about each rendered list item. When you update a list, React needs to determine what has changed. You could have added, removed, re-arranged, or updated the list's items.

Imagine transitioning from

```html
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

to

```html
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

In addition to the updated counts, a human reading this would probably say that you swapped Alexa and Ben's ordering and inserted Claudia between Alexa and Ben. However, React is a computer program and does not know what you intended, so you need to specify a _key_ property for each list item to differentiate each list item from its siblings. If your data was from a database, Alexa, Ben, and Claudia's database IDs could be used as keys.

```js {1}
<li key={user.id}>
  {user.name}: {user.taskCount} tasks left
</li>
```

When a list is re-rendered, React takes each list item's key and searches the previous list's items for a matching key. If the current list has a key that didn't exist before, React creates a component. If the current list is missing a key that existed in the previous list, React destroys the previous component. If two keys match, the corresponding component is moved.

Keys tell React about the identity of each component, which allows React to maintain state between re-renders. If a component's key changes, the component will be destroyed and re-created with a new state.

`key` is a special and reserved property in React. When an element is created, React extracts the `key` property and stores the key directly on the returned element. Even though `key` may look like it is passed as props, React automatically uses `key` to decide which components to update. There's no way for a component to ask what `key` its parent specified.

**It's strongly recommended that you assign proper keys whenever you build dynamic lists.** If you don't have an appropriate key, you may want to consider restructuring your data so that you do.

If no key is specified, React will report an error and use the array index as a key by default. Using the array index as a key is problematic when trying to re-order a list's items or inserting/removing list items. Explicitly passing `key={i}` silences the error but has the same problems as array indices and is not recommended in most cases.

Keys do not need to be globally unique; they only need to be unique between components and their siblings.

### Implementing time travel {/*implementing-time-travel*/}

In the tic-tac-toe game's history, each past move has a unique ID associated with it: it's the sequential number of the move. Moves will never be re-ordered, deleted, or inserted in the middle, so it's safe to use the move index as a key.

In the `Game` function, you can add the key as `<li key={move}>`, and if you reload the rendered game, React's "key" error should disappear:

```js {4}
const moves = history.map((squares, move) => {
  //...
  return (
    <li key={move}>
      <button onClick={() => jumpTo(move)}>{description}</button>
    </li>
  );
});
```

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const currentSquares = history[history.length - 1];

  function handlePlay(nextSquares) {
    setHistory([...history, nextSquares]);
    setXIsNext(!xIsNext);
  }

  function jumpTo(nextMove) {
    // TODO
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li key={move}>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}

```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}

.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

Before you can implement `jumpTo`, you need the `Game` component to keep track of which step the user is currently viewing. To do this, define a new state variable called `currentMove`, defaulting to `0`:

```js {4}
export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const currentSquares = history[history.length - 1];
  //...
}
```

Next, update the `jumpTo` function inside `Game` to update that `currentMove`. You'll also set `xIsNext` to `true` if the number that you're changing `currentMove` to is even.

```js {4-5}
export default function Game() {
  // ...
  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
    setXIsNext(nextMove % 2 === 0);
  }
  //...
}
```

You will now make two changes to the `Game`'s `handlePlay` function which is called when you click on a square.

- If you "go back in time" and then make a new move from that point, you only want to keep the history up to that point. Instead of adding `nextSquares` after all items (`...` spread syntax) in `history`, you'll add it after all items in `history.slice(0, currentMove + 1)` so that you're only keeping that portion of the old history.
- Each time a move is made, you need to update `currentMove` to point to the latest history entry.

```js {2-4}
function handlePlay(nextSquares) {
  const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
  setHistory(nextHistory);
  setCurrentMove(nextHistory.length - 1);
  setXIsNext(!xIsNext);
}
```

Finally, you will modify the `Game` component to render the currently selected move, instead of always rendering the final move:

```js {5}
export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const currentSquares = history[currentMove];

  // ...
}
```

If you click on any step in the game's history, the tic-tac-toe board should immediately update to show what the board looked like after that step occurred.

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({value, onSquareClick}) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [xIsNext, setXIsNext] = useState(true);
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const currentSquares = history[currentMove];

  function handlePlay(nextSquares) {
    const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
    setHistory(nextHistory);
    setCurrentMove(nextHistory.length - 1);
    setXIsNext(!xIsNext);
  }

  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
    setXIsNext(nextMove % 2 === 0);
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li key={move}>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

### Final cleanup {/*final-cleanup*/}

If you look at the code very closely, you may notice that `xIsNext === true` when `currentMove` is even and `xIsNext === false` when `currentMove` is odd. In other words, if you know the value of `currentMove`, then you can always figure out what `xIsNext` should be.

There's no reason for you to store both of these in state. In fact, always try to avoid redundant state. Simplifying what you store in state reduces bugs and makes your code easier to understand. Change `Game` so that it doesn't store `xIsNext` as a separate state variable and instead figures it out based on the `currentMove`:

```js {4,11,15}
export default function Game() {
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const xIsNext = currentMove % 2 === 0;
  const currentSquares = history[currentMove];

  function handlePlay(nextSquares) {
    const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
    setHistory(nextHistory);
    setCurrentMove(nextHistory.length - 1);
  }

  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
  }
  // ...
}
```

You no longer need the `xIsNext` state declaration or the calls to `setXIsNext`. Now, there's no chance for `xIsNext` to get out of sync with `currentMove`, even if you make a mistake while coding the components.

### Wrapping up {/*wrapping-up*/}

Congratulations! You've created a tic-tac-toe game that:

- Lets you play tic-tac-toe,
- Indicates when a player has won the game,
- Stores a game's history as a game progresses,
- Allows players to review a game's history and see previous versions of a game's board.

Nice work! We hope you now feel like you have a decent grasp of how React works.

Check out the final result here:

<Sandpack>

```js src/App.js
import { useState } from 'react';

function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

export default function Game() {
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const xIsNext = currentMove % 2 === 0;
  const currentSquares = history[currentMove];

  function handlePlay(nextSquares) {
    const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
    setHistory(nextHistory);
    setCurrentMove(nextHistory.length - 1);
  }

  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li key={move}>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

```css src/styles.css
* {
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  margin: 20px;
  padding: 0;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.board-row:after {
  clear: both;
  content: '';
  display: table;
}

.status {
  margin-bottom: 10px;
}
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
```

</Sandpack>

If you have extra time or want to practice your new React skills, here are some ideas for improvements that you could make to the tic-tac-toe game, listed in order of increasing difficulty:

1. For the current move only, show "You are at move #..." instead of a button.
1. Rewrite `Board` to use two loops to make the squares instead of hardcoding them.
1. Add a toggle button that lets you sort the moves in either ascending or descending order.
1. When someone wins, highlight the three squares that caused the win (and when no one wins, display a message about the result being a draw).
1. Display the location for each move in the format (row, col) in the move history list.

Throughout this tutorial, you've touched on React concepts including elements, components, props, and state. Now that you've seen how these concepts work when building a game, check out [Thinking in React](/learn/thinking-in-react) to see how the same React concepts work when build an app's UI.
