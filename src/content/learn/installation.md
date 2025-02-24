---
title: ఇన్స్టలేషన్
---

<Intro>

React ను దశలవారీగా ఉపయోగించడానికి రూపొందించారు. మీ అవసరానికి అనుగుణంగా React ను కొంచెం లేదా ఎక్కువగా ఉపయోగించవచ్చు. React అంటే ఏమిటో తెలుసుకోవాలనుకుంటున్నారా, HTML పేజీకి ఇన్‌టరాక్టివిటీ జోడించాలనుకుంటున్నారా, లేదా ఒక పెద్ద React యాప్‌ను రూపొందించాలనుకుంటున్నారా? అయితే, ఈ విభాగం మీకు సహాయపడుతుంది.

</Intro>

## React ను ట్రై చేయండి {/*try-react*/}

React తో పని చేయడానికి మీరు ఏమీ ఇన్‌స్టాల్ చేయాల్సిన అవసరం లేదు. ఈ సాండ్‌బాక్స్‌ను ఎడిట్ చేసి చూడండి!

<Sandpack>

```js
function Greeting({ name }) {
  return <h1>హలో, {name}</h1>;
}

export default function App() {
  return <Greeting name="వరల్డ్" />
}
```

</Sandpack>

మీరు దీన్ని డైరెక్ట్ గా ఎడిట్ చేయవచ్చు లేదా కుడి పైభాగంలో ఉన్న "Fork" బటన్‌ని నొక్కి కొత్త టాబ్‌లో తెరవచ్చు.

React డాక్యుమెంటేషన్‌లోని చాలా పేజీలు ఇలాంటి సాండ్‌బాక్స్‌లను కలిగి ఉంటాయి. React డాక్యుమెంటేషన్ బయట కూడా React ను సపోర్ట్ చేసే అనేక ఆన్‌లైన్ సాండ్‌బాక్స్‌లు ఉన్నాయి: ఉదాహరణకు, [CodeSandbox](https://codesandbox.io/s/new), [StackBlitz](https://stackblitz.com/fork/react), లేదా [CodePen.](https://codepen.io/pen?template=QWYVwWN)

మీ కంప్యూటర్‌లో React ను ప్రయత్నించాలంటే, [ఈ HTML పేజీని డౌన్లోడ్ చేయండి.](https://gist.githubusercontent.com/gaearon/0275b1e1518599bbeafcde4722e79ed1/raw/db72dcbf3384ee1708c4a07d3be79860db04bff0/example.html) దీన్ని మీ ఎడిటర్‌లో మరియు బ్రౌజర్‌లో ఓపెన్ చేయండి!

## React యాప్‌ను సృష్టించడం {/*creating-a-react-app*/}

కొత్త React యాప్‌ను ప్రారంభించాలని అనుకుంటే, మీరు సిఫార్సు చేసిన ఫ్రేమ్‌వర్క్‌ను ఉపయోగించి [React యాప్‌ను సృష్టించవచ్చు](/learn/creating-a-react-app).

<<<<<<< HEAD
## React ఫ్రేమ్‌వర్క్‌ను నిర్మించడం {/*build-a-react-framework*/}

మీ ప్రాజెక్ట్‌కు ఏ ఫ్రేమ్‌వర్క్ సరిపోకపోతే, లేదా మీరు మీ స్వంత ఫ్రేమ్‌వర్క్ నిర్మించడం ప్రారంభించాలనుకుంటే, [మీ స్వంత React ఫ్రేమ్‌వర్క్‌ను నిర్మించండి](/learn/building-a-react-framework).
=======
## Build a React App from Scratch {/*build-a-react-app-from-scratch*/}

If a framework is not a good fit for your project, you prefer to build your own framework, or you just want to learn the basics of a React app you can [build a React app from scratch](/learn/build-a-react-app-from-scratch).
>>>>>>> fc29603434ec04621139738f4740caed89d659a7

## ఇప్పటికే ఉన్న ప్రాజెక్ట్‌కు React జోడించండి {/*add-react-to-an-existing-project*/}

మీ ప్రస్తుత యాప్ లేదా వెబ్‌సైట్‌లో React ను ఉపయోగించాలనుకుంటే, [ఇప్పటికే ఉన్న ప్రాజెక్ట్‌కు React జోడించండి.](/learn/add-react-to-an-existing-project)

<<<<<<< HEAD
## వాడుక లో లేని ఆప్షన్స్ {/*deprecated-options*/}

### Create React App (వాడుకలో లేదు) {/*create-react-app-deprecated*/}

Create React App అనేది ఒక పాత టూల్, కొత్త React యాప్‌లను రూపొందించడానికి ఇంతకుముందు సిఫార్సు చేయబడేది. మీరు కొత్త React యాప్‌ను ప్రారంభించాలని అనుకుంటే, [React యాప్‌ను క్రియేట్ చేయడం](/learn/creating-a-react-app) లో సిఫార్సు చేసిన ఫ్రేమ్‌వర్క్‌ను ఉపయోగించవచ్చు.

మరిన్ని వివరాల కోసం, [Sunsetting Create React App](/blog/2025/02/14/sunsetting-create-react-app) చూడండి.
=======

<Note>

#### Should I use Create React App? {/*should-i-use-create-react-app*/}

No. Create React App has been deprecated. For more information, see [Sunsetting Create React App](/blog/2025/02/14/sunsetting-create-react-app).

</Note>
>>>>>>> fc29603434ec04621139738f4740caed89d659a7

## తదుపరి చర్యలు {/*next-steps*/}

React లో మీరు ప్రతిరోజూ ఎదుర్కొనే ముఖ్యమైన కాన్సెప్ట్స్‌ను పరిచయం చేయడానికి [క్విక్ స్టార్ట్](/learn) గైడ్‌ను సందర్శించండి.
