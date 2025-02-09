---
title: ఇంటరాక్టివిటీ ని జోడించటం
---

<Intro>

యూజర్ ఇన్పుట్కు రెస్పాన్స్ గా స్క్రీన్‌పై కొన్ని అంశాలు అప్‌డేట్ చేయబడతాయి. ఉదాహరణకు, ఇమేజ్ గ్యాలరీని క్లిక్ చేయడం వలన యాక్టివ్ ఇమేజ్ స్విచ్ చేయబడుతుంది. React లో, కాలక్రమేణా మారే డేటాను *state* అంటారు. మీరు ఏదైనా కాంపోనెంట్కి state ని జోడించవచ్చు మరియు అవసరమైన విధంగా దాన్ని అప్డేట్ చేయవచ్చు. ఈ చాప్టర్లో, ఇంట్రాక్షన్స్ ని హేండిల్ చేయడం, వాటి state ని అప్డేట్ చేయడం మరియు కాలక్రమేణా డిఫరెంట్ అవుట్‌పుట్‌లను డిస్ప్లే చేసే కాంపోనెంట్లను ఎలా వ్రాయాలో మీరు నేర్చుకుంటారు.

</Intro>


<YouWillLearn isChapter={true}>

* [యూజర్ ఇనిషియేట్ చేసిన ఈవెంట్‌లను ఎలా హేండిల్ చేయాలి](/learn/responding-to-events)
* [state తో ఇన్ఫర్మేషన్ ని "గుర్తుంచుకోవడానికి" కాంపోనెంట్లను ఎలా తయారు చేయాలి](/learn/state-a-components-memory)
* [React ఎలా UI ని రెండు ఫేసెస్ లో అప్‌డేట్ చేస్తుంది](/learn/render-and-commit)
* [మీరు మార్చిన వెంటనే state ఎందుకు అప్డేట్ అవ్వడు](/learn/state-as-a-snapshot)
* [మల్టిపుల్ state అప్డేట్లను ఎలా క్యూ లో ఉంచాలి](/learn/queueing-a-series-of-state-updates)
* [state లో ఉన్న ఆబ్జెక్ట్ ను ఎలా అప్‌డేట్ చేయాలి](/learn/updating-objects-in-state)
* [state లో array ని ఎలా అప్‌డేట్ చేయాలి](/learn/updating-arrays-in-state)

</YouWillLearn>

## ఈవెంట్స్ కి రెస్పాండ్ అవ్వడం {/*responding-to-events*/}

మీ JSX కి *ఈవెంట్ హ్యాండ్లర్‌లను* జోడించడానికి React మిమ్మల్ని అనుమతిస్తుంది. ఈవెంట్ హ్యాండ్లర్లు అనేవి మీ స్వంత ఫంక్షన్‌లు ఇవి క్లిక్ చేయడం, హోవర్ చేయడం, ఫోర్మ్ ఇన్పుట్ల పై ఫోకస్ చేయడం మొదలైన యూజర్ ఇంట్రాక్షన్స్కి రెస్పాన్స్ గా ట్రిగ్గర్ చేయబడతాయి.

`<button>` వంటి బిల్ట్-ఇన్ కాంపోనెంట్లు `onClick` వంటి బిల్ట్-ఇన్ బ్రౌజర్ ఈవెంట్‌లకు మాత్రమే సపోర్ట్ చేస్తాయి. అయితే, మీరు మీ స్వంత కాంపోనెంట్లను కూడా క్రియేట్ చేయొచ్చు మరియు వారి ఈవెంట్ హ్యాండ్లర్ props కు మీరు ఇష్టపడే ఏదైనా అప్లికేషన్-స్పెసిఫిక్ పేర్లను ఇవ్వవచ్చు.


<Sandpack>

```js
export default function App() {
  return (
    <Toolbar
      onPlayMovie={() => alert('Playing!')}
      onUploadImage={() => alert('Uploading!')}
    />
  );
}

function Toolbar({ onPlayMovie, onUploadImage }) {
  return (
    <div>
      <Button onClick={onPlayMovie}>
        Play Movie
      </Button>
      <Button onClick={onUploadImage}>
        Upload Image
      </Button>
    </div>
  );
}

function Button({ onClick, children }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}
```

```css
button { margin-right: 10px; }
```

</Sandpack>

<LearnMore path="/learn/responding-to-events">

ఈవెంట్ హ్యాండ్లర్‌లను ఎలా జోడించాలో తెలుసుకోవడానికి **[ఈవెంట్‌లకు రెస్పాండ్ అవ్వడం](/learn/responding-to-events)** గురించి చదవండి.

</LearnMore>

## state: ఒక కాంపోనెంట్ యొక్క మెమరీ {/*state-a-components-memory*/}

ఇంట్రాక్షన్స్ కి ఫలితంగా స్క్రీన్‌పై ఉన్న వాటిని కాంపోనెంట్లు తరచుగా మార్చవలసి ఉంటుంది. ఫోర్మ్లో టైప్ చేయడం అనేది ఇన్పుట్ ఫీల్డ్‌ను అప్‌డేట్ చేయాలి, ఇమేజ్ కరౌసెల్ పై "నెక్స్ట్" ని క్లిక్ చేయడం ద్వారా ఏ ఇమేజ్ ప్రదర్శించబడుతుందో మార్చాలి, "కొనుగోలు" పై క్లిక్ చేసినప్పుడు షాపింగ్ కార్ట్‌లో ప్రోడక్ట్ ని ఉంచాలి. కాంపోనెంట్లు విషయాలను "గుర్తుంచుకోవాలి": ప్రస్తుత ఇన్పుట్ వేల్యూ, ప్రస్తుత ఇమేజ్, షాపింగ్ కార్ట్. React లో, ఈ రకమైన కాంపోనెంట్-నిర్దిష్ట మెమరీని *state* అంటారు.

మీరు ఒక కాంపోనెంట్కి [`useState`](/reference/react/useState) హుక్ ద్వారా state ని జోడించవచ్చు. *హుక్స్* అనేవి మీ కాంపోనెంట్లు React ఫీచర్‌లను ఉపయోగించడానికి అనుమతించే ప్రత్యేక ఫంక్షన్లు (ఆ ఫీచర్లలో state ఒకటి). `useState` హుక్ state వేరియబుల్‌ని డిక్లేర్ చేయడానికి మిమ్మల్ని అనుమతిస్తుంది. ఇది ఇనీటియాల్ state ని తీసుకుంటుంది మరియు ఒక పెయిర్ అఫ్ వాల్యూస్ ని రిటర్న్ చేస్తుంది: ప్రస్తుత state మరియు దానిని అప్‌డేట్ చేయడానికి మిమ్మల్ని అనుమతించే state సెట్టర్ ఫంక్షన్.

```js
const [index, setIndex] = useState(0);
const [showMore, setShowMore] = useState(false);
```

ఇమేజ్ గ్యాలరీ క్లిక్‌ పై state ని ఎలా ఉపయోగిస్తుంది మరియు అప్‌డేట్ చేస్తుందో ఇక్కడ చూడండి:

<Sandpack>

```js
import { useState } from 'react';
import { sculptureList } from './data.js';

export default function Gallery() {
  const [index, setIndex] = useState(0);
  const [showMore, setShowMore] = useState(false);
  const hasNext = index < sculptureList.length - 1;

  function handleNextClick() {
    if (hasNext) {
      setIndex(index + 1);
    } else {
      setIndex(0);
    }
  }

  function handleMoreClick() {
    setShowMore(!showMore);
  }

  let sculpture = sculptureList[index];
  return (
    <>
      <button onClick={handleNextClick}>
        Next
      </button>
      <h2>
        <i>{sculpture.name} </i>
        by {sculpture.artist}
      </h2>
      <h3>
        ({index + 1} of {sculptureList.length})
      </h3>
      <button onClick={handleMoreClick}>
        {showMore ? 'Hide' : 'Show'} details
      </button>
      {showMore && <p>{sculpture.description}</p>}
      <img
        src={sculpture.url}
        alt={sculpture.alt}
      />
    </>
  );
}
```

```js src/data.js
export const sculptureList = [{
  name: 'Homenaje a la Neurocirugía',
  artist: 'Marta Colvin Andrade',
  description: 'Although Colvin is predominantly known for abstract themes that allude to pre-Hispanic symbols, this gigantic sculpture, an homage to neurosurgery, is one of her most recognizable public art pieces.',
  url: 'https://i.imgur.com/Mx7dA2Y.jpg',
  alt: 'A bronze statue of two crossed hands delicately holding a human brain in their fingertips.'
}, {
  name: 'Floralis Genérica',
  artist: 'Eduardo Catalano',
  description: 'This enormous (75 ft. or 23m) silver flower is located in Buenos Aires. It is designed to move, closing its petals in the evening or when strong winds blow and opening them in the morning.',
  url: 'https://i.imgur.com/ZF6s192m.jpg',
  alt: 'A gigantic metallic flower sculpture with reflective mirror-like petals and strong stamens.'
}, {
  name: 'Eternal Presence',
  artist: 'John Woodrow Wilson',
  description: 'Wilson was known for his preoccupation with equality, social justice, as well as the essential and spiritual qualities of humankind. This massive (7ft. or 2,13m) bronze represents what he described as "a symbolic Black presence infused with a sense of universal humanity."',
  url: 'https://i.imgur.com/aTtVpES.jpg',
  alt: 'The sculpture depicting a human head seems ever-present and solemn. It radiates calm and serenity.'
}, {
  name: 'Moai',
  artist: 'Unknown Artist',
  description: 'Located on the Easter Island, there are 1,000 moai, or extant monumental statues, created by the early Rapa Nui people, which some believe represented deified ancestors.',
  url: 'https://i.imgur.com/RCwLEoQm.jpg',
  alt: 'Three monumental stone busts with the heads that are disproportionately large with somber faces.'
}, {
  name: 'Blue Nana',
  artist: 'Niki de Saint Phalle',
  description: 'The Nanas are triumphant creatures, symbols of femininity and maternity. Initially, Saint Phalle used fabric and found objects for the Nanas, and later on introduced polyester to achieve a more vibrant effect.',
  url: 'https://i.imgur.com/Sd1AgUOm.jpg',
  alt: 'A large mosaic sculpture of a whimsical dancing female figure in a colorful costume emanating joy.'
}, {
  name: 'Ultimate Form',
  artist: 'Barbara Hepworth',
  description: 'This abstract bronze sculpture is a part of The Family of Man series located at Yorkshire Sculpture Park. Hepworth chose not to create literal representations of the world but developed abstract forms inspired by people and landscapes.',
  url: 'https://i.imgur.com/2heNQDcm.jpg',
  alt: 'A tall sculpture made of three elements stacked on each other reminding of a human figure.'
}, {
  name: 'Cavaliere',
  artist: 'Lamidi Olonade Fakeye',
  description: "Descended from four generations of woodcarvers, Fakeye's work blended traditional and contemporary Yoruba themes.",
  url: 'https://i.imgur.com/wIdGuZwm.png',
  alt: 'An intricate wood sculpture of a warrior with a focused face on a horse adorned with patterns.'
}, {
  name: 'Big Bellies',
  artist: 'Alina Szapocznikow',
  description: "Szapocznikow is known for her sculptures of the fragmented body as a metaphor for the fragility and impermanence of youth and beauty. This sculpture depicts two very realistic large bellies stacked on top of each other, each around five feet (1,5m) tall.",
  url: 'https://i.imgur.com/AlHTAdDm.jpg',
  alt: 'The sculpture reminds a cascade of folds, quite different from bellies in classical sculptures.'
}, {
  name: 'Terracotta Army',
  artist: 'Unknown Artist',
  description: 'The Terracotta Army is a collection of terracotta sculptures depicting the armies of Qin Shi Huang, the first Emperor of China. The army consisted of more than 8,000 soldiers, 130 chariots with 520 horses, and 150 cavalry horses.',
  url: 'https://i.imgur.com/HMFmH6m.jpg',
  alt: '12 terracotta sculptures of solemn warriors, each with a unique facial expression and armor.'
}, {
  name: 'Lunar Landscape',
  artist: 'Louise Nevelson',
  description: 'Nevelson was known for scavenging objects from New York City debris, which she would later assemble into monumental constructions. In this one, she used disparate parts like a bedpost, juggling pin, and seat fragment, nailing and gluing them into boxes that reflect the influence of Cubism’s geometric abstraction of space and form.',
  url: 'https://i.imgur.com/rN7hY6om.jpg',
  alt: 'A black matte sculpture where the individual elements are initially indistinguishable.'
}, {
  name: 'Aureole',
  artist: 'Ranjani Shettar',
  description: 'Shettar merges the traditional and the modern, the natural and the industrial. Her art focuses on the relationship between man and nature. Her work was described as compelling both abstractly and figuratively, gravity defying, and a "fine synthesis of unlikely materials."',
  url: 'https://i.imgur.com/okTpbHhm.jpg',
  alt: 'A pale wire-like sculpture mounted on concrete wall and descending on the floor. It appears light.'
}, {
  name: 'Hippos',
  artist: 'Taipei Zoo',
  description: 'The Taipei Zoo commissioned a Hippo Square featuring submerged hippos at play.',
  url: 'https://i.imgur.com/6o5Vuyu.jpg',
  alt: 'A group of bronze hippo sculptures emerging from the sett sidewalk as if they were swimming.'
}];
```

```css
h2 { margin-top: 10px; margin-bottom: 0; }
h3 {
 margin-top: 5px;
 font-weight: normal;
 font-size: 100%;
}
img { width: 120px; height: 120px; }
button {
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
```

</Sandpack>

<LearnMore path="/learn/state-a-components-memory">

వేల్యూ ను ఎలా గుర్తుంచుకోవాలి మరియు ఇంటరాక్షన్ పై దాన్ని ఎలా అప్డేట్ చేయాలో తెలుసుకోవడానికి [స్టేట్: ఎ కాంపోనెంట్స్ మెమరీ](/learn/state-a-components-memory) ని చదవండి.

</LearnMore>

## రెండర్ అండ్ కమిట్ {/*render-and-commit*/}

మీ కాంపోనెంట్లు స్క్రీన్‌ పై ప్రదర్శించబడటానికి ముందు, అవి తప్పనిసరిగా React ద్వారా రెండర్ చేయబడాలి. ఈ ప్రాసెస్ లోని స్టెప్స్ ను అర్థం చేసుకోవడం వల్ల మీ కోడ్ ఎలా ఎగ్జిక్యూట్ చేయబడుతుందో తెలుసుకోవడానికి మరియు దాని ప్రవర్తనను వివరించడానికి మీకు సహాయపడుతుంది.

మీ కాంపోనెంట్లు కిచెన్ లో కూక్స్ అని ఊహించుకోండి, అవి పదార్థాల నుండి రుచికరమైన వంటకాలను తయారు చేస్తున్నాయి. ఈ స్కీనారియోలో, React అనేది కస్టమర్ల నుండి రిక్వెస్ట్లను తీసుకుని వారి ఆర్డర్‌లను వారికి సర్వ్ చేసే వెయిటర్. UI ని రిక్వెస్ట్ మరియు సర్వ్ చేయడం అనే ఈ ప్రక్రియ మూడు స్టెప్స్ను కలిగి ఉంటుంది:

1. **ట్రిగరింగ్** రెండర్ (డైనర్ యొక్క ఆర్డర్‌ను వంటగదికి డెలివర్ చేయడం)
2. **రెండరింగ్** కాంపోనెంట్ (వంటగదిలో ఆర్డర్‌ను సిద్ధం చేయడం)
3. DOM కి **కమిట్** చేయడం (ఆర్డర్‌ను టేబుల్‌ పై ఉంచడం)

<IllustrationBlock sequential>
  <Illustration caption="ట్రిగ్గర్" alt="ఒక రెస్టారెంట్‌లో React సర్వర్‌గా, యూజర్ల నుండి ఆర్డర్‌లను తీసుకోవడం మరియు వాటిని కాంపోనెంట్ కిచెన్‌కు డెలివరీ చేయడం." src="/images/docs/illustrations/i_render-and-commit1.png" />
  <Illustration caption="Render" alt="The Card Chef gives React a fresh Card component." src="/images/docs/illustrations/i_render-and-commit2.png" />
  <Illustration caption="Commit" alt="React delivers the Card to the user at their table." src="/images/docs/illustrations/i_render-and-commit3.png" />
</IllustrationBlock>

<LearnMore path="/learn/render-and-commit">

UI అప్‌డేట్ లైఫ్ సైకిల్ ని తెలుసుకోవడానికి **[రెండర్ అండ్ కమిట్](/learn/render-and-commit)** ని చదవండి.

</LearnMore>

## state ఒక స్నాప్‌షాట్ {/*state-as-a-snapshot*/}

సాధారణ JavaScript వేరియబుల్స్ కాకుండా, React state స్నాప్‌షాట్ లాగా ప్రవర్తిస్తుంది. దీన్ని సెట్ చేయడం వలన మీరు ఇప్పటికే కలిగి ఉన్న state వేరియబుల్ మారదు, బదులుగా రీ-రెండర్‌ను ప్రేరేపిస్తుంది. ఇది మొదట ఆశ్చర్యం కలిగించవచ్చు!

```js
console.log(count);  // 0
setCount(count + 1); // 1 తో రీ-రెండర్‌ని రిక్వెస్ట్ చేయండి
console.log(count);  // ఇప్పటికీ 0!
```

ఈ ప్రవర్తన మీకు సూక్ష్మ బగ్లను నివారించడంలో సహాయపడుతుంది. ఇక్కడ ఒక చిన్న చాట్ యాప్ ఉంది. మీరు ముందుగా "సెండ్" నొక్కి, *తరువాత* రెసెప్పెంట్ను బాబ్‌గా మార్చినట్లయితే ఏమి జరుగుతుందో ఊహించడానికి ప్రయత్నించండి. ఐదు సెకన్ల తర్వాత `alert` లో ఎవరి పేరు కనిపిస్తుంది?

<Sandpack>

```js
import { useState } from 'react';

export default function Form() {
  const [to, setTo] = useState('Alice');
  const [message, setMessage] = useState('Hello');

  function handleSubmit(e) {
    e.preventDefault();
    setTimeout(() => {
      alert(`You said ${message} to ${to}`);
    }, 5000);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        To:{' '}
        <select
          value={to}
          onChange={e => setTo(e.target.value)}>
          <option value="Alice">Alice</option>
          <option value="Bob">Bob</option>
        </select>
      </label>
      <textarea
        placeholder="Message"
        value={message}
        onChange={e => setMessage(e.target.value)}
      />
      <button type="submit">Send</button>
    </form>
  );
}
```

```css
label, textarea { margin-bottom: 10px; display: block; }
```

</Sandpack>


<LearnMore path="/learn/state-as-a-snapshot">
  
ఈవెంట్ హ్యాండ్లర్‌లలో state ఎందుకు "స్థిరంగా" మరియు మారకుండా కనిపిస్తుందో తెలుసుకోవడానికి **[state ఒక స్నాప్‌షాట్](/learn/state-as-a-snapshot)** ని చదవండి.

</LearnMore>

## state అప్‌డేట్‌ల సెట్‌ను క్రమబద్ధీకరించడం {/*queueing-a-series-of-state-updates*/}

ఈ కాంపోనెంట్ బగ్గా ఉంది: '+3' పై క్లిక్ చేసినప్పుడు స్కోరును ఒకసారి మాత్రమే పెంచుతుంది.

<Sandpack>

```js
import { useState } from 'react';

export default function Counter() {
  const [score, setScore] = useState(0);

  function increment() {
    setScore(score + 1);
  }

  return (
    <>
      <button onClick={() => increment()}>+1</button>
      <button onClick={() => {
        increment();
        increment();
        increment();
      }}>+3</button>
      <h1>Score: {score}</h1>
    </>
  )
}
```

```css
button { display: inline-block; margin: 10px; font-size: 20px; }
```

</Sandpack>

[state ఒక స్నాప్‌షాట్](/learn/state-as-a-snapshot) ఇది ఎందుకు జరుగుతుందో వివరిస్తుంది. state ని సెట్ చేయడం కొత్త రీ-రెండర్‌ను రిక్వెస్ట్ చేస్తుంది, కానీ ఇప్పటికే రన్ అవుతున్న కోడ్‌లో దాన్ని మార్చదు. కాబట్టి మీరు `setScore(score + 1)` ని కాల్ చేసిన వెంటనే `score` `0` గా కొనసాగుతుంది.


```js
console.log(score);  // 0
setScore(score + 1); // setScore(0 + 1);
console.log(score);  // 0
setScore(score + 1); // setScore(0 + 1);
console.log(score);  // 0
setScore(score + 1); // setScore(0 + 1);
console.log(score);  // 0
```

మీరు state ని సెట్ చేసేటప్పుడు *అప్‌డేటర్ ఫంక్షన్* ని పాస్ చేయడం ద్వారా దీన్ని పరిష్కరించవచ్చు. `setScore(score + 1)` ని `setScore(s => s + 1)` తో రీప్లేస్ చేయడం ద్వారా అది "+3" బటన్‌ను ఎలా ఫిక్స్ చేస్తుందో గమనించండి. ఇది మల్టిపుల్ state అప్డేట్లను క్కు చేయడానికి మిమ్మల్ని అనుమతిస్తుంది.


<Sandpack>

```js
import { useState } from 'react';

export default function Counter() {
  const [score, setScore] = useState(0);

  function increment() {
    setScore(s => s + 1);
  }

  return (
    <>
      <button onClick={() => increment()}>+1</button>
      <button onClick={() => {
        increment();
        increment();
        increment();
      }}>+3</button>
      <h1>Score: {score}</h1>
    </>
  )
}
```

```css
button { display: inline-block; margin: 10px; font-size: 20px; }
```

</Sandpack>

<LearnMore path="/learn/queueing-a-series-of-state-updates">

state అప్‌డేట్‌ల సీక్వెన్స్ ని ఎలా క్యూలో ఉంచాలో తెలుసుకోవడానికి **[state అప్‌డేట్‌ల సెట్‌ను క్రమబద్ధీకరించడం](/learn/queueing-a-series-of-state-updates)** గురించి చదవండి.

</LearnMore>

## state లో ఆబ్జెక్ట్‌లను అప్‌డేట్ చేయడం {/*updating-objects-in-state*/}

state ఆబ్జెక్ట్‌లతో సహా ఎలాంటి JavaScript వేల్యూ ని అయినా కలిగి ఉంటుంది. కానీ మీరు డైరెక్ట్ గా React state లో ఉంచే ఆబ్జెక్ట్లను మరియు array లను చేంజ్ చేయకూడదు. బదులుగా, మీరు ఆబ్జెక్ట్ మరియు array ని అప్‌డేట్ చేయాలనుకున్నప్పుడు, మీరు కొత్తదాన్ని సృష్టించాలి (లేదా ఇప్పటికే ఉన్న దాని కాపీని తయారు చేయాలి), ఆపై ఆ కాపీని ఉపయోగించడానికి state ను అప్‌డేట్ చేయాలి.


సాధారణంగా, మీరు మార్చాలనుకుంటున్న ఆబ్జెక్ట్లు మరియు array లను కాపీ చేయడానికి మీరు `...` స్ప్రెడ్ సింటాక్స్‌ని ఉపయోగిస్తారు. ఉదాహరణకు, నెస్టెడ్ ఆబ్జెక్ట్ ను అప్డేట్ చేయడం ఇలా ఉంటుంది:

<Sandpack>

```js
import { useState } from 'react';

export default function Form() {
  const [person, setPerson] = useState({
    name: 'Niki de Saint Phalle',
    artwork: {
      title: 'Blue Nana',
      city: 'Hamburg',
      image: 'https://i.imgur.com/Sd1AgUOm.jpg',
    }
  });

  function handleNameChange(e) {
    setPerson({
      ...person,
      name: e.target.value
    });
  }

  function handleTitleChange(e) {
    setPerson({
      ...person,
      artwork: {
        ...person.artwork,
        title: e.target.value
      }
    });
  }

  function handleCityChange(e) {
    setPerson({
      ...person,
      artwork: {
        ...person.artwork,
        city: e.target.value
      }
    });
  }

  function handleImageChange(e) {
    setPerson({
      ...person,
      artwork: {
        ...person.artwork,
        image: e.target.value
      }
    });
  }

  return (
    <>
      <label>
        Name:
        <input
          value={person.name}
          onChange={handleNameChange}
        />
      </label>
      <label>
        Title:
        <input
          value={person.artwork.title}
          onChange={handleTitleChange}
        />
      </label>
      <label>
        City:
        <input
          value={person.artwork.city}
          onChange={handleCityChange}
        />
      </label>
      <label>
        Image:
        <input
          value={person.artwork.image}
          onChange={handleImageChange}
        />
      </label>
      <p>
        <i>{person.artwork.title}</i>
        {' by '}
        {person.name}
        <br />
        (located in {person.artwork.city})
      </p>
      <img
        src={person.artwork.image}
        alt={person.artwork.title}
      />
    </>
  );
}
```

```css
label { display: block; }
input { margin-left: 5px; margin-bottom: 5px; }
img { width: 200px; height: 200px; }
```

</Sandpack>

ఆబ్జెక్ట్‌లను కోడ్‌లో కాపీ చేయడం విసుగు తెప్పిస్తే, రిపిటీటివ్ కోడ్‌ను తగ్గించడానికి మీరు [Immer](https://github.com/immerjs/use-immer) అనే లైబ్రరీని ఉపయోగించవచ్చు:

<Sandpack>

```js
import { useImmer } from 'use-immer';

export default function Form() {
  const [person, updatePerson] = useImmer({
    name: 'Niki de Saint Phalle',
    artwork: {
      title: 'Blue Nana',
      city: 'Hamburg',
      image: 'https://i.imgur.com/Sd1AgUOm.jpg',
    }
  });

  function handleNameChange(e) {
    updatePerson(draft => {
      draft.name = e.target.value;
    });
  }

  function handleTitleChange(e) {
    updatePerson(draft => {
      draft.artwork.title = e.target.value;
    });
  }

  function handleCityChange(e) {
    updatePerson(draft => {
      draft.artwork.city = e.target.value;
    });
  }

  function handleImageChange(e) {
    updatePerson(draft => {
      draft.artwork.image = e.target.value;
    });
  }

  return (
    <>
      <label>
        Name:
        <input
          value={person.name}
          onChange={handleNameChange}
        />
      </label>
      <label>
        Title:
        <input
          value={person.artwork.title}
          onChange={handleTitleChange}
        />
      </label>
      <label>
        City:
        <input
          value={person.artwork.city}
          onChange={handleCityChange}
        />
      </label>
      <label>
        Image:
        <input
          value={person.artwork.image}
          onChange={handleImageChange}
        />
      </label>
      <p>
        <i>{person.artwork.title}</i>
        {' by '}
        {person.name}
        <br />
        (located in {person.artwork.city})
      </p>
      <img
        src={person.artwork.image}
        alt={person.artwork.title}
      />
    </>
  );
}
```

```json package.json
{
  "dependencies": {
    "immer": "1.7.3",
    "react": "latest",
    "react-dom": "latest",
    "react-scripts": "latest",
    "use-immer": "0.5.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

```css
label { display: block; }
input { margin-left: 5px; margin-bottom: 5px; }
img { width: 200px; height: 200px; }
```

</Sandpack>

<LearnMore path="/learn/updating-objects-in-state">

ఆబ్జెక్ట్‌లను కరెక్ట్ గా ఎలా అప్‌డేట్ చేయాలో తెలుసుకోవడానికి **[state లో ఆబ్జెక్ట్‌లను అప్‌డేట్ చేయడం](/learn/updating-objects-in-state)** గురించి చదవండి.

</LearnMore>

## state లో array లను అప్డేట్ చేయడం {/*updating-arrays-in-state*/}

array లు అనేవి మీరు state లో స్టోర్ చేయగల మరొక రకమైన మ్యుటేబుల్ JavaScript ఆబ్జెక్ట్‌లు మరియు వాటిని రీడ్-ఓన్లీ గా మాత్రమే పరిగణించాలి. ఆబ్జెక్ట్‌ల మాదిరిగానే, మీరు store లో స్టోర్ చేయబడిన array ని అప్‌డేట్ చేయాలనుకున్నప్పుడు, మీరు కొత్తదాన్ని సృష్టించాలి (లేదా ఇప్పటికే ఉన్న దాని కాపీని తయారు చేయాలి), ఆపై కొత్త array ని ఉపయోగించడానికి state ని సెట్ చేయాలి:

<Sandpack>

```js
import { useState } from 'react';

const initialList = [
  { id: 0, title: 'Big Bellies', seen: false },
  { id: 1, title: 'Lunar Landscape', seen: false },
  { id: 2, title: 'Terracotta Army', seen: true },
];

export default function BucketList() {
  const [list, setList] = useState(
    initialList
  );

  function handleToggle(artworkId, nextSeen) {
    setList(list.map(artwork => {
      if (artwork.id === artworkId) {
        return { ...artwork, seen: nextSeen };
      } else {
        return artwork;
      }
    }));
  }

  return (
    <>
      <h1>Art Bucket List</h1>
      <h2>My list of art to see:</h2>
      <ItemList
        artworks={list}
        onToggle={handleToggle} />
    </>
  );
}

function ItemList({ artworks, onToggle }) {
  return (
    <ul>
      {artworks.map(artwork => (
        <li key={artwork.id}>
          <label>
            <input
              type="checkbox"
              checked={artwork.seen}
              onChange={e => {
                onToggle(
                  artwork.id,
                  e.target.checked
                );
              }}
            />
            {artwork.title}
          </label>
        </li>
      ))}
    </ul>
  );
}
```

</Sandpack>

కోడ్‌లో array లను కాపీ చేయడం విసుగు తెప్పిస్తే, రిపిటీటివ్ కోడ్‌ను తగ్గించడానికి మీరు [Immer](https://github.com/immerjs/use-immer) అనే లైబ్రరీని ఉపయోగించవచ్చు:

<Sandpack>

```js
import { useState } from 'react';
import { useImmer } from 'use-immer';

const initialList = [
  { id: 0, title: 'Big Bellies', seen: false },
  { id: 1, title: 'Lunar Landscape', seen: false },
  { id: 2, title: 'Terracotta Army', seen: true },
];

export default function BucketList() {
  const [list, updateList] = useImmer(initialList);

  function handleToggle(artworkId, nextSeen) {
    updateList(draft => {
      const artwork = draft.find(a =>
        a.id === artworkId
      );
      artwork.seen = nextSeen;
    });
  }

  return (
    <>
      <h1>Art Bucket List</h1>
      <h2>My list of art to see:</h2>
      <ItemList
        artworks={list}
        onToggle={handleToggle} />
    </>
  );
}

function ItemList({ artworks, onToggle }) {
  return (
    <ul>
      {artworks.map(artwork => (
        <li key={artwork.id}>
          <label>
            <input
              type="checkbox"
              checked={artwork.seen}
              onChange={e => {
                onToggle(
                  artwork.id,
                  e.target.checked
                );
              }}
            />
            {artwork.title}
          </label>
        </li>
      ))}
    </ul>
  );
}
```

```json package.json
{
  "dependencies": {
    "immer": "1.7.3",
    "react": "latest",
    "react-dom": "latest",
    "react-scripts": "latest",
    "use-immer": "0.5.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

</Sandpack>

<LearnMore path="/learn/updating-arrays-in-state">

array లను సరిగ్గా ఎలా అప్‌డేట్ చేయాలో తెలుసుకోవడానికి **[state లో array లను అప్‌డేట్ చేయడం](/learn/updating-arrays-in-state)** గురించి చదవండి.

</LearnMore>

## తరవాత ఏంటి? {/*whats-next*/}

ఈ చాప్టర్ ని పేజీలవారీగా చదవడం ప్రారంభించడానికి [ఈవెంట్లకు రెస్పాండ్ అవ్వడం](/learn/responding-to-events) కి వెళ్లండి!

లేదా, మీకు ఈ టాపిక్స్ గురించి ఇప్పటికే తెలిసి ఉంటే, [మేనేజింగ్ state](/learn/managing-state) గురించి ఎందుకు చదవకూడదు?
