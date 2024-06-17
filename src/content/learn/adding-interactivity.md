---
శీర్షిక: ఇంటరాక్టివిటీ చేయడం
---

<Intro>

వినియోగదారు ఇన్పుట్ నుండి స్క్రీన్‌పై కొనసాగుతున్న కొన్ని విషయాలు అదనపు అప్‌డేట్ అవుతాయి. ఉదా, చిత్ర గ్యాలరీని ప్రేస్ చేసినప్పుడు యాక్టివ్ చిత్రాన్ని మార్చుకోవచ్చు. రియాక్ట్‌లో, సమయం పైన మారుతున్న డేటాను *స్టేట్ం* అని పిలిచించబడుతుంది. ఏమైనా మంత్రాలును యొక్క మేరకు స్థితిని జోడించవచ్చు, మరియు అవసరం అయితే అదనపుగా అప్‌డేట్ చేయవచ్చు. ఈ అధ్యాయంలో, మనం ఇంటరక్షన్‌లను చేర్చే, అవస్థను నవీకరించే మరియు సమయంలో వేర్వేరు ఔట్‌పుట్‌లను ప్రదర్శించే కాంపోనెంట్‌లను ఎలా రాయాలో వెళ్ళండి.

</Intro>


<YouWillLearn isChapter={true}>

* [వినియోగదారు ప్రారంభించిన సంఘటనలను ఎలా నిర్వహించాలి అనే విషయం గురించి ఎలాగో ఇది](/learn/responding-to-events)
* [కంపోనెంట్‌లలో స్థితితో సమాచారాన్ని 'గుర్తుచేయడం' ఎలా చేయాలి అనే విషయం గురించి ఎలాగో ఇది](/learn/state-a-components-memory)
* [రియాక్ట్ UI ని రెండు దశల్లో ఎలా అప్‌డేట్ చేస్తుంది](/learn/render-and-commit)
* [మీరు మార్చిన వెంటనే స్టేట్ం ఎందుకు నవీకరించబడదు](/learn/state-as-a-snapshot)
* [బహుళ స్టేట్ం నవీకరణలను ఎలా వరుసలో ఉంచాలి](/learn/queueing-a-series-of-state-updates)
* [స్టేట్ం ఉన్న వస్తువును ఎలా అప్‌డేట్ చేయాలి](/learn/updating-objects-in-state)
* [స్టేట్ం శ్రేణిని ఎలా అప్‌డేట్ చేయాలి](/learn/updating-arrays-in-state)

</YouWillLearn>

## సంఘటనలపై స్పందిస్తున్నారు {/*responding-to-events*/}

మీ JSXకి *ఈవెంట్ హ్యాండ్లర్‌లను* జోడించడానికి రియాక్ట్ మిమ్మల్ని అనుమతిస్తుంది. ఈవెంట్ హ్యాండ్లర్లు మీ స్వంత ఫంక్షన్‌లు, క్లిక్ చేయడం, హోవర్ చేయడం, ఫారమ్ ఇన్‌పుట్‌లపై దృష్టి పెట్టడం మొదలైన వినియోగదారు పరస్పర చర్యలకు ప్రతిస్పందనగా ట్రిగ్గర్ చేయబడతాయి.

`<button>` వంటి అంతర్నిర్మిత భాగాలు `onClick` వంటి అంతర్నిర్మిత బ్రౌజర్ ఈవెంట్‌లకు మాత్రమే మద్దతు ఇస్తాయి. అయితే, మీరు మీ స్వంత భాగాలను కూడా సృష్టించవచ్చు మరియు వారి ఈవెంట్ హ్యాండ్లర్ ప్రాప్‌లకు మీరు ఇష్టపడే ఏదైనా అప్లికేషన్-నిర్దిష్ట పేర్లను ఇవ్వవచ్చు.


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

చదవండి **[ఈవెంట్స్‌పై స్పందిస్తున్నారు](/learn/responding-to-events)** ఈవెంట్ హ్యాండ్లర్‌లను ఎలా జోడించాలో తెలుసుకోవడానికి.

</LearnMore>

## స్టేట్ం: ఒక భాగం యొక్క మెమరీ {/*state-a-components-memory*/}

పరస్పర చర్య ఫలితంగా స్క్రీన్‌పై ఉన్న వాటిని భాగాలు తరచుగా మార్చవలసి ఉంటుంది. ఫారమ్‌లో టైప్ చేయడం ఇన్‌పుట్ ఫీల్డ్‌ను అప్‌డేట్ చేయాలి, ఇమేజ్ రంగులరాట్నంపై "తదుపరి" క్లిక్ చేయడం ద్వారా ఏ చిత్రం ప్రదర్శించబడుతుందో మార్చాలి, "కొనుగోలు" క్లిక్ చేయడం షాపింగ్ కార్ట్‌లో ఉత్పత్తిని ఉంచుతుంది. భాగాలు విషయాలను "గుర్తుంచుకోవాలి": ప్రస్తుత ఇన్‌పుట్ విలువ, ప్రస్తుత చిత్రం, షాపింగ్ కార్ట్. రియాక్ట్‌లో, ఈ రకమైన కాంపోనెంట్-నిర్దిష్ట మెమరీని *స్టేట్* అంటారు.

మీరు ఒక భాగానికి స్థితిని జోడించవచ్చు [`useState`](/reference/react/useState) హుక్. *హుక్స్* అనేది మీ భాగాలు రియాక్ట్ ఫీచర్‌లను ఉపయోగించడానికి అనుమతించే ప్రత్యేక విధులు (ఆ లక్షణాలలో రాష్ట్రం ఒకటి). `useState` హుక్ స్టేట్ వేరియబుల్‌ని ప్రకటించడానికి మిమ్మల్ని అనుమతిస్తుంది. ఇది ప్రారంభ స్థితిని తీసుకుంటుంది మరియు ఒక జత విలువలను అందిస్తుంది: ప్రస్తుత స్థితి మరియు దానిని అప్‌డేట్ చేయడానికి మిమ్మల్ని అనుమతించే స్టేట్ సెట్టర్ ఫంక్షన్.

```js
const [index, setIndex] = useState(0);
const [showMore, setShowMore] = useState(false);
```

క్లిక్‌పై ఇమేజ్ గ్యాలరీ ఎలా ఉపయోగిస్తుంది మరియు అప్‌డేట్‌ల స్టేట్ంని ఇక్కడ చూడండి:

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

విలువను ఎలా గుర్తుంచుకోవాలి మరియు పరస్పర చర్యపై దాన్ని ఎలా నవీకరించాలో తెలుసుకోవడానికి **[స్టేట్: ఎ కాంపోనెంట్స్ మెమరీ](/నేర్చుకోండి/స్టేట్-ఎ-కాంపోనెంట్స్-మెమరీ)** చదవండి.

</LearnMore>

## రెండర్ మరియు కామిట్ {/*render-and-commit*/}

మీ భాగాలు స్క్రీన్‌పై ప్రదర్శించబడటానికి ముందు, అవి తప్పనిసరిగా రియాక్ట్ ద్వారా రెండర్ చేయబడాలి. ఈ ప్రక్రియలోని దశలను అర్థం చేసుకోవడం మీ కోడ్ ఎలా అమలు చేయబడుతుందో మరియు దాని ప్రవర్తనను వివరించడానికి మీకు సహాయపడుతుంది.

మీ భాగాలు వంటగదిలో ఉడుకుతున్నాయని ఊహించండి, పదార్థాల నుండి రుచికరమైన వంటకాలను సమీకరించండి. ఈ దృష్టాంతంలో, రియాక్ట్ అనేది కస్టమర్ల నుండి అభ్యర్థనలను ఉంచే మరియు వారి ఆర్డర్‌లను వారికి అందించే వెయిటర్. UI ని అభ్యర్థించడం మరియు అందించడం అనే ఈ ప్రక్రియ మూడు దశలను కలిగి ఉంటుంది:

1. **ట్రిగరింగ్** రెండర్ (డైనర్ ఆర్డర్‌ను వంటగదికి అందించడం)
2. **రెండరింగ్** భాగం (వంటగదిలో ఆర్డర్‌ను సిద్ధం చేయడం)
3. **కామిట్ చేస్తున్నారు** DOM కి (ఆర్డర్‌ను టేబుల్‌పై ఉంచడం)

<IllustrationBlock sequential>
  <Illustration caption="Trigger" alt="React as a server in a restaurant, fetching orders from the users and delivering them to the Component Kitchen." src="/images/docs/illustrations/i_render-and-commit1.png" />
  <Illustration caption="Render" alt="The Card Chef gives React a fresh Card component." src="/images/docs/illustrations/i_render-and-commit2.png" />
  <Illustration caption="Commit" alt="React delivers the Card to the user at their table." src="/images/docs/illustrations/i_render-and-commit3.png" />
</IllustrationBlock>

<LearnMore path="/learn/render-and-commit">

UI అప్‌డేట్ జీవితచక్రాన్ని తెలుసుకోవడానికి **[రెండర్ మరియు కమిట్](/నేర్చుకోండి/రెండర్-మరియు-కమిట్)** చదవండి.

</LearnMore>

## స్నాప్‌షాట్‌గా స్టేట్ం {/*state-as-a-snapshot*/}

సాధారణ జావాస్క్రిప్ట్ వేరియబుల్స్ కాకుండా, రియాక్ట్ స్టేట్ స్నాప్‌షాట్ లాగా ప్రవర్తిస్తుంది. దీన్ని సెట్ చేయడం వలన మీరు ఇప్పటికే కలిగి ఉన్న స్టేట్ వేరియబుల్ మారదు, బదులుగా రీ-రెండర్‌ను ప్రేరేపిస్తుంది. ఇది మొదట ఆశ్చర్యం కలిగించవచ్చు!

```js
console.log(count);  // 0
setCount(count + 1); // Request a re-render with 1
console.log(count);  // Still 0!
```

ఈ ప్రవర్తన మీకు సూక్ష్మ దోషాలను నివారించడంలో సహాయపడుతుంది. ఇక్కడ ఒక చిన్న చాట్ యాప్ ఉంది. మీరు ముందుగా "Send" నొక్కి, *then* గ్రహీతను బాబ్‌గా మార్చినట్లయితే ఏమి జరుగుతుందో ఊహించడానికి ప్రయత్నించండి. ఐదు సెకన్ల తర్వాత `alert`లో ఎవరి పేరు కనిపిస్తుంది?


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
  
ఈవెంట్ హ్యాండ్లర్‌లలో రాష్ట్రం ఎందుకు "fixed" మరియు మారకుండా కనిపిస్తుందో తెలుసుకోవడానికి **[స్నాప్‌షాట్‌గా స్థితి](/నేర్చుకోండి/స్టేట్-ఎ-స్నాప్‌షాట్)** చదవండి.

</LearnMore>

## రాష్ట్ర నవీకరణల శ్రేణిని వరుసలో ఉంచడం {/*queueing-a-series-of-state-updates*/}

ఈ కాంపోనెంట్ బగ్గా ఉంది: '+3' పై క్లిక్ చేసి స్కోరును ఒకసారిమాత్రమే పెంచుతుంది.

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

[స్నాప్‌షాట్ గా స్థితి](/learn/state-as-a-snapshot) అది అన్ని ఏమీ జరుగుతోందనే వివరిస్తుంది. స్థితి సెట్ చేయడం కొనసాగితే, కొత్త రీ-రెండర్ అభ్యర్థనను అభ్యర్థిస్తుంది, కానీ ఇప్పటికే పనిచేస్తున్న కోడ్‌లో అది మారనింది. కాబట్టి `setScore(score + 1)` ను కల చేసిన తరువాత, `score` `0` మాత్రమే ఉండేది.


```js
console.log(score);  // 0
setScore(score + 1); // setScore(0 + 1);
console.log(score);  // 0
setScore(score + 1); // setScore(0 + 1);
console.log(score);  // 0
setScore(score + 1); // setScore(0 + 1);
console.log(score);  // 0
```

మీరు స్థితిని సెట్ చేస్తాయినప్పుడు *అప్‌డేటర్ ఫంక్షన్* పాస్ చేయడందరికీ ఈ సమస్యను సరిచేయవచ్చు. గమనించండి హాయిగా `setScore(score + 1)` ను `setScore(s => s + 1)` తో మార్చినప్పుడు "+3" బటన్ సరిగ్గా కనిపిస్తుంది. ఇది మరియుండు మరికొన్ని స్థితి నవీకరణలను మేరకు చేసే అవకాశం ఇస్తుంది.


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

స్టేట్ అప్‌డేట్‌ల క్రమాన్ని ఎలా క్యూలో ఉంచాలో తెలుసుకోవడానికి **[స్టేట్ అప్‌డేట్‌ల శ్రేణిని వరుసలో ఉంచడం](/నేర్చుకోండి/క్యూయింగ్-a-series-of-state-updates)** చదవండి.

</LearnMore>

## స్టేట్ట్రంలోని వస్తువులను నవీకరిస్తోంది {/*updating-objects-in-state*/}

రియాక్ట్ స్టేట్ ఏదైనా రకంలో జావాస్క్రిప్ట్ విలువను ధరించవచ్చు, స్థితిలో నిలువాలు మరియు అర్రేలు మార్చడానికి డైరెక్ట్‌గా మారాలేదు. స్టేట్ట్రంలో అనివాసించే వస్తువులను మరియు అర్రేలను నవీకరించడానికి, మీరు కొనసాగుతున్న కొత్తవిను సృష్టించండి (లేదా ఇప్పటికే ఉండేవాటిని నకలి చేయండి), మరియు ఆ కోపిని ఉపయోగించి స్టేట్ట్రంని నవీకరించండి.


సాధారణంగా, మీరు మార్చడానికి కొనసాగుతున్న వస్తువులను కాపీ చేయడానికి `...` విస్తరణ సింటాక్స్‌ను వాడవచ్చు. ఉదాహరణకు, ఒక అడుగులో ఉన్న వస్తువును నవీకరించుటకు ఇలా ఉండవచ్చు:

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

ఆబ్జెక్ట్‌లను కోడ్‌లో కాపీ చేయడం విసుగు తెప్పిస్తే, పునరావృత కోడ్‌ను తగ్గించడానికి మీరు [Immer](https://github.com/immerjs/use-immer) వంటి లైబ్రరీని ఉపయోగించవచ్చు:

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

వస్తువులను సరిగ్గా ఎలా అప్‌డేట్ చేయాలో తెలుసుకోవడానికి **[రాష్ట్రంలో ఆబ్జెక్ట్‌లను అప్‌డేట్ చేయడం](/నేర్చుకోండి/అప్‌డేటింగ్-ఆబ్జెక్ట్స్-ఇన్-స్టేట్)** చదవండి.

</LearnMore>

## స్థితిలో వరుసలను నవీకరించడం {/*updating-arrays-in-state*/}

వరుసలు స్థితిలో భద్రమయంగా స్థానికీకరించవచ్చు. వస్తువులతో సమానంగా, స్థితిలో భద్రమయంగా ఉండాలని నీతిని అనుకుంటాం. స్థితిలో ఉన్న ఒక వరుసను నవీకరించడానికి, మీరు కొత్తవను సృష్టించండి (లేదా ఇప్పటికే ఉండేవాటిని నకలి చేయండి), అప్పుడు స్థితిని కొత్త వరుసతో ఉపయోగించడానికి వస్తువులను సెట్ చేయండి:

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

కోడ్‌లో శ్రేణులను కాపీ చేయడం విసుగు తెప్పిస్తే, పునరావృత కోడ్‌ను తగ్గించడానికి మీరు [Immer](https://github.com/immerjs/use-immer) వంటి లైబ్రరీని ఉపయోగించవచ్చు:

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

శ్రేణులను సరిగ్గా ఎలా అప్‌డేట్ చేయాలో తెలుసుకోవడానికి **[రాష్ట్రంలో శ్రేణులను అప్‌డేట్ చేయడం](/learn/updating-arrays-in-state)** చదవండి.

</LearnMore>

## తరవాత ఏంటి? {/*whats-next*/}

ఈ అధ్యాయాన్ని పేజీలవారీగా చదవడం ప్రారంభించడానికి [ఈవెంట్‌లకు ప్రతిస్పందించడం](/learn/responding-to-events)కి వెళ్లండి!

లేదా, మీకు ఈ అంశాల గురించి ఇప్పటికే తెలిసి ఉంటే, [మేనేజింగ్ స్టేట్](/learn/managing-state) గురించి ఎందుకు చదవకూడదు?
