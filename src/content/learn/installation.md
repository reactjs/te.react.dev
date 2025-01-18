---
title: ఇన్స్టలేషన్
---

<Intro>

React ను దశలవారీగా ఉపయోగించడానికి రూపొందించారు. మీ అవసరానికి అనుగుణంగా React ను కొంచెం లేదా ఎక్కువగా ఉపయోగించవచ్చు. React అంటే ఏమిటో తెలుసుకోవాలనుకుంటున్నారా, HTML పేజీకి ఇన్‌టరాక్టివిటీ జోడించాలనుకుంటున్నారా, లేదా ఒక పెద్ద React యాప్‌ను రూపొందించాలనుకుంటున్నారా? అయితే, ఈ విభాగం మీకు సహాయపడుతుంది.

</Intro>

<YouWillLearn isChapter={true}>

* [కొత్త React ప్రాజెక్ట్‌ను ఎలా ప్రారంభించాలి](/learn/start-a-new-react-project)
* [React ను ఇప్పటికే ఉన్న ప్రాజెక్ట్‌కు ఎలా జోడించాలి](/learn/add-react-to-an-existing-project)
* [మీ ఎడిటర్‌ను ఎలా సెటప్ చేయాలి](/learn/editor-setup)
* [React Developer Tools ను ఎలా ఇన్‌స్టాల్ చేయాలి](/learn/react-developer-tools)

</YouWillLearn>

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

You can edit it directly or open it in a new tab by pressing the "Fork" button in the upper right corner.

Most pages in the React documentation contain sandboxes like this. Outside of the React documentation, there are many online sandboxes that support React: for example, [CodeSandbox](https://codesandbox.io/s/new), [StackBlitz](https://stackblitz.com/fork/react), or [CodePen.](https://codepen.io/pen?template=QWYVwWN)

### Try React locally {/*try-react-locally*/}

To try React locally on your computer, [download this HTML page.](https://gist.githubusercontent.com/gaearon/0275b1e1518599bbeafcde4722e79ed1/raw/db72dcbf3384ee1708c4a07d3be79860db04bff0/example.html) Open it in your editor and in your browser!

## Start a new React project {/*start-a-new-react-project*/}

If you want to build an app or a website fully with React, [start a new React project.](/learn/start-a-new-react-project)

## Add React to an existing project {/*add-react-to-an-existing-project*/}

If want to try using React in your existing app or a website, [add React to an existing project.](/learn/add-react-to-an-existing-project)

## Next steps {/*next-steps*/}

Head to the [Quick Start](/learn) guide for a tour of the most important React concepts you will encounter every day.

