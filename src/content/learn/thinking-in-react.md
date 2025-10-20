---
title: React లాగా ఆలోచించడం
---

<Intro>

మీరు చూసే డిజైన్‌లు మరియు మీరు రూపొందించే యాప్‌ల గురించి మీరు ఏమనుకుంటున్నారో React మార్చగలదు. మీరు React తో UI ను రూపొందించినప్పుడు, మీరు ముందుగా దాన్ని *కాంపోనెంట్స్* అని పిలిచే ముక్కలుగా విడదీస్తారు. అప్పుడు, మీరు మీ ప్రతి కాంపోనెంట్కి సంబంధించిన విభిన్న విసువల్ స్టేట్లను వివరిస్తారు. చివరగా, మీరు మీ కాంపోనెంట్లను ఒకదానితో ఒకటి కనెక్ట్ చేస్తారు, తద్వారా డేటా వాటి ద్వారా ప్రవహిస్తుంది. ఈ ట్యుటోరియల్‌లో, React తో సెర్చ్ చేయగల ప్రోడక్ట్ డేటా టేబుల్ ను రూపొందించే ఆలోచన ప్రక్రియ ద్వారా మేము మీకు మార్గనిర్దేశం చేస్తాము.

</Intro>

## మోకప్‌తో ప్రారంభించండి {/*start-with-the-mockup*/}

మీరు ఇప్పటికే JSON API ని మరియు డిజైనర్ నుండి ఒక మోకప్ ని కలిగి ఉన్నారని ఊహించుకోండి.

JSON API ఇలా కనిపించే కొంత డేటాను రిటర్న్ చేస్తుంది:

```json
[
  { category: "Fruits", price: "$1", stocked: true, name: "Apple" },
  { category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit" },
  { category: "Fruits", price: "$2", stocked: false, name: "Passionfruit" },
  { category: "Vegetables", price: "$2", stocked: true, name: "Spinach" },
  { category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin" },
  { category: "Vegetables", price: "$1", stocked: true, name: "Peas" }
]
```

మోకప్ ఇలా కనిపిస్తుంది:

<img src="/images/docs/s_thinking-in-react_ui.png" width="300" style={{margin: '0 auto'}} />

React లో UI ని ఇంప్లిమెంట్ చేయడానికి, మీరు సాధారణంగా అదే ఐదు దశలను అనుసరిస్తారు.

## స్టెప్ 1: UI ని కాంపోనెంట్ హైరార్కి గా విభజించండి {/*step-1-break-the-ui-into-a-component-hierarchy*/}

మోకప్‌లోని ప్రతి కాంపోనెంట్ మరియు సబ్ కాంపోనెంట్ల చుట్టూ బాక్స్లను గీయడం మరియు వాటికి పేరు పెట్టడం ద్వారా ప్రారంభించండి. మీరు డిజైనర్‌తో పని చేస్తే, వారు తమ డిజైన్ టూల్‌లో ఈ కాంపోనెంట్లకు ఇప్పటికే పేరు పేరుపెట్టి ఉండవచ్చు. వాళ్ళని అడగండి!

మీ నేపథ్యాన్ని బట్టి, మీరు డిజైన్‌ను వివిధ మార్గాల్లో కాంపోనెంట్లుగా విభజించడం గురించి ఆలోచించవచ్చు:

* **ప్రోగ్రామింగ్**--మీరు కొత్త ఫంక్షన్ లేదా ఆబ్జెక్ట్‌ని క్రియేట్ చేయాలా వద్దా అని నిర్ణయించడానికి అదే టెక్నిక్లను ఉపయోగించండి. అటువంటి టెక్నాలజీ అనేది [సెపరేషన్ ఆఫ్ కన్సర్న్](https://en.wikipedia.org/wiki/Separation_of_concerns), అంటే, ఒక కాంపోనెంట్ ఐడియల్ గా ఒక విషయం గురించి మాత్రమే ఆందోళన చెందాలి. అది పెద్ద కాంపోనెంట్గా పెరుగుతూ ఉంటే, దానిని చిన్న సబ్ కాంపోనెంట్లుగా డీకంపోస్ చేయాలి.
* **CSS**--మీరు క్లాస్ సెలెక్టర్‌లను దేని కోసం తయారు చేస్తారో పరిగణించండి. (అయినప్పటికీ, కాంపోనెంట్లు కొద్దిగా తక్కువగా ఉంటాయి)
* **డిజైన్**--మీరు డిజైన్ యొక్క లేయర్‌లను ఎలా ఆర్గనైజ్ చేయాలో పరిశీలించండి.

మీ JSON బాగా స్ట్రక్చర్ చేయబడినట్లయితే, అది మీ UI యొక్క కాంపోనెంట్ స్ట్రక్చర్‌కు సహజంగా మ్యాప్ చేయబడుతుందని మీరు తరచుగా కనుగొంటారు. ఎందుకంటే UI మరియు డేటా మోడల్‌లు తరచుగా ఒకే రకమైన ఇన్ఫర్మేషన్ ఆర్కిటెక్చర్ ని కలిగి ఉంటాయి--అంటే, సేమ్ షేప్. మీ UI ని కాంపోనెంట్లుగా విభజించండి, ఇక్కడ ప్రతి కాంపోనెంట్ మీ డేటా మోడల్‌లోని ఒక కాంపోనెంట్కి మ్యాచ్ అవుతుంది.

ఈ స్క్రీన్‌లో ఐదు కాంపోనెంట్లు ఉన్నాయి:

<FullWidth>

<CodeDiagram flip>

<img src="/images/docs/s_thinking-in-react_ui_outline.png" width="500" style={{margin: '0 auto'}} />

1. `FilterableProductTable` (గ్రెయ్) మొత్తం యాప్‌ను కలిగి ఉంది.
2. `SearchBar` (నీలం) యూజర్ ఇన్‌పుట్ ను రిసీవ్ చేసుకుంటుంది.
3. `ProductTable` (లావెండర్) యూజర్ ఇన్‌పుట్ ప్రకారం లిస్ట్ ను ప్రదర్శిస్తుంది మరియు ఫిల్టర్ చేస్తుంది.
4. `ProductCategoryRow` (ఆకుపచ్చ) ప్రతి కెటిగోరి కి హెడ్డింగ్ ను ప్రదర్శిస్తుంది.
5. `ProductRow`	(పసుపు) ప్రతి ప్రోడక్ట్ కి రో (row) ను ప్రదర్శిస్తుంది.

</CodeDiagram>

</FullWidth>

మీరు `ProductTable` (లావెండర్) ని చూస్తే, టేబుల్ హెడర్ ("Name" మరియు "Price" లేబుల్‌లను కలిగి ఉంటుంది) దాని స్వంత కాంపోనెంట్ కాదని మీరు చూస్తారు. ఇది ప్రాధాన్యతకు సంబంధించిన విషయం మరియు మీరు ఏ విధంగానైనా వెళ్ళవచ్చు. ఈ ఉదాహరణ కోసం, ఇది `ProductTable` లో ఒక కాంపోనెంట్ ఎందుకంటే ఇది `ProductTable` యొక్క లిస్ట్ లో కనిపిస్తుంది. అయితే, ఈ హెడర్ సంక్లిష్టంగా పెరిగితే (ఉదా., మీరు సార్టింగ్‌ని జోడిస్తే), మీరు దానిని దాని స్వంత `ProductTableHeader` కాంపోనెంట్లోకి తరలించవచ్చు.

ఇప్పుడు మీరు మోకప్‌లోని కాంపోనెంట్లను గుర్తించారు, వాటిని హైరార్కి పరంగా అమర్చండి. మోకప్‌లోని మరొక కాంపోనెంట్లో కనిపించే కాంపోనెంట్లు హైరార్కి లో చైల్డ్ గా కనిపించాలి:

* `FilterableProductTable`
    * `SearchBar`
    * `ProductTable`
        * `ProductCategoryRow`
        * `ProductRow`

## స్టెప్ 2: React లో స్టాటిక్ వెర్షన్‌ను బిల్డ్ చేయండి {/*step-2-build-a-static-version-in-react*/}

ఇప్పుడు మీరు మీ కాంపోనెంట్ హైరార్కి ని కలిగి ఉన్నారు, మీ యాప్‌ని ఇంప్లిమెంట్ చేయడానికి ఇది సమయం. ఎటువంటి ఇంటరాక్టివిటీని జోడించకుండానే మీ డేటా మోడల్ నుండి UI ని అందించే వెర్షన్ ను బిల్డ్ చేయడం చాలా సరళమైన విధానం. మొదట స్టాటిక్ వెర్షన్‌ను బిల్డ్ చేయడం మరియు తర్వాత ఇంటరాక్టివిటీని జోడించడం చాలా సులభం. స్టాటిక్ వెర్షన్‌ను రూపొందించడానికి చాలా టైపింగ్ అవసరం మరియు ఆలోచన అవసరం లేదు, కానీ ఇంటరాక్టివిటీని జోడించడానికి చాలా ఆలోచన అవసరం మరియు ఎక్కువ టైపింగ్ కాదు.

మీ డేటా మోడల్‌ను రెండర్ చేసే మీ యాప్ యొక్క స్టాటిక్ వెర్షన్‌ను రూపొందించడానికి, మీరు ఇతర కాంపోనెంట్లను రీయూస్ చేయాలి మరియు [props](/learn/passing-props-to-a-component) ను ఉపయోగించి డేటాను పాస్ చేసే [కాంపోనెంట్లను](/learn/your-first-component) బిల్డ్ చేయాలనుకుంటున్నారు. props అనేది పేరెంట్ నుండి చైల్డ్ కు డేటాను పంపే మార్గం. (మీకు [state](/learn/state-a-components-memory) అనే కాన్సెప్ట్ బాగా తెలిసి ఉంటే, ఈ స్టాటిక్ వెర్షన్‌ని బిల్డ్ చేయడానికి స్టేట్‌ని అస్సలు ఉపయోగించవద్దు. state ఇంటరాక్టివిటీకి మాత్రమే రిజర్వ్ చేయబడింది, అంటే కాలక్రమేణా మారే డేటా. ఈ యాప్ స్టాటిక్ వెర్షన్ కాబట్టి, మీకు state అవసరం లేదు.)

మీరు హైరార్కి లో (`FilterableProductTable` వంటి) టాప్ కాంపోనెంట్లను బిడ్ల్ చేయడం ప్రారంభించడం ద్వారా "టాప్ డౌన్" లేదా దిగువ కాంపోనెంట్ల నుండి (`ProductRow` వంటివి) పని చేయడం ద్వారా "బాటమ్ అప్" నిర్మించవచ్చు. సింపుల్ ఉదాహరణలలో, సాధారణంగా పైకి-క్రిందికి వెళ్లడం సులభం మరియు పెద్ద ప్రాజెక్ట్‌లలో, దిగువ నుండి పైకి వెళ్లడం సులభం.

<Sandpack>

```jsx src/App.js
function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar() {
  return (
    <form>
      <input type="text" placeholder="Search..." />
      <label>
        <input type="checkbox" />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

function FilterableProductTable({ products }) {
  return (
    <div>
      <SearchBar />
      <ProductTable products={products} />
    </div>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding-top: 10px;
}
td {
  padding: 2px;
  padding-right: 40px;
}
```

</Sandpack>

(ఈ కోడ్ కష్టంగా అనిపిస్తే, ముందుగా [క్విక్ స్టార్ట్](/learn/) ద్వారా వెళ్లండి!)

మీ కాంపోనెంట్లను బిల్డ్ చేసిన తర్వాత, మీ డేటా మోడల్‌ను రెండర్ చేసే రీయూజబుల్ కాంపోనెంట్ల లైబ్రరీని మీరు కలిగి ఉంటారు. ఇది స్టాటిక్ యాప్ అయినందున, కాంపోనెంట్‌లు JSX ని మాత్రమే రిటర్న్ చేస్తాయి. హైరార్కి టాప్ లో ఉన్న కాంపోనెంట్ (`FilterableProductTable`) మీ డేటా మోడల్‌ను props గా తీసుకుంటుంది. దీన్నే _వన్-వే డేటా ఫ్లో_ అంటారు ఎందుకంటే డేటా టాప్-లెవల్ కాంపోనెంట్ నుండి ట్రీ లో దిగువన ఉన్న వాటికి ప్రవహిస్తుంది.

<Pitfall>

ఈ సమయంలో, మీరు ఎటువంటి state వాల్యూస్ ను ఉపయోగించకూడదు. అది తదుపరి దశ కోసం!

</Pitfall>

## స్టెప్ 3: మీ UI state ని కనిష్టంగా మరియు పూర్తిగా రిప్రసెంట్ చేయడానికి ఒక మార్గాన్ని కనుగొనండి {/*step-3-find-the-minimal-but-complete-representation-of-ui-state*/}

UI ఇంటరాక్టివ్‌గా చేయడానికి, మీరు మీ అండర్లయింగ్ డేటా మోడల్‌ని మార్చడానికి యూసర్లను అనుమతించాలి. మీరు దీని కోసం *state* ని ఉపయోగిస్తారు.

మీ యాప్ గుర్తుంచుకోవాల్సిన డేటాను మార్చే మినిమల్ సెట్‌గా state గురించి ఆలోచించండి. state ని స్ట్రక్చర్ చేయడానికి అత్యంత ముఖ్యమైన సూత్రం దానిని [DRY (డోంట్ రిపీట్ యూర్సెల్ఫ్)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) గా ఉంచడం. మీ అప్లికేషన్‌కు అవసరమైన state యొక్క అబ్సొల్యూట్ మినిమల్ రిప్రజెంటేషన్ ను గుర్తించండి మరియు మిగతావన్నీ డిమాండ్‌పై కంప్యూట్ చేయండి. ఉదాహరణకు, మీరు షాపింగ్ లిస్ట్ ను బిల్డ్ చేస్తున్నట్లైతే, మీరు ఐటమ్స్ ను state లో array గా స్టోర్ చేయవచ్చు. మీరు లిస్ట్ లోని ఐటెమ్‌ల సంఖ్యను కూడా డిస్ప్లే చేయాలనుకుంటే, ఐటెమ్‌ల సంఖ్యను మరొక state వేల్యూ గా స్టోర్ చేయవద్దు - బదులుగా, మీ array లెన్త్ ను చదవండి.

ఇప్పుడు ఈ ఉదాహరణ అప్లికేషన్‌లోని అన్ని డేటా ముక్కల గురించి ఆలోచించండి:

1. ప్రొడక్టుల ఒరిజినల్ లిస్ట్
2. యూజర్ ఎంటర్ చేసిన సెర్చ్ టెక్స్ట్
3. చెక్‌బాక్స్ వేల్యూ
4. ఫిల్టర్ చేసిన ప్రొడక్ట్స్ లిస్ట్

వీటిలో state ఏది? దయచేసి state కానిది ఏమిటో గుర్తించండి:

* ఇది కాలక్రమేణా **మారకుండా** ఉంటుందా? అలా అయితే, అది state కాదు.
* ఇది **పేరెంట్ నుండి** props ద్వారా పంపబడిందా? అలా అయితే, అది state కాదు.
* **మీరు దీన్ని కంప్యూట్ చేయగలరా** ఇప్పటికే ఉన్న state లేదా మీ కాంపోనెంట్‌లోని props ఆధారంగా? అలా అయితే, ఇది *ఖచ్చితంగా* state కాదు!

మిగిలి ఉన్నది బహుశా state మాత్రమే.

వాటిని ఒక్కొక్కటిగా మళ్లీ చూద్దాం:

1. ప్రొడక్ట్స్ యొక్క ఒరిజినల్ లిస్ట్ **props గా పాస్ చేయబడింది, కనుక ఇది state కాదు.** 
2. కాలక్రమేణా మారుతున్నందున సెర్చ్ టెక్స్ట్ state గా కనిపిస్తోంది మరియు దేని నుండి కంప్యూట్ చేయబడదు.
3. చెక్‌బాక్స్ వేల్యూ కాలానుగుణంగా మారుతూ ఉంటుంది మరియు దేని నుండి కంప్యూట్ చేయబడదు కాబట్టి దాని వేల్యూ state గా కనిపిస్తోంది.
4. ప్రొడక్ట్స్ యొక్క ఫిల్టర్ చేయబడిన లిస్ట్ **state కాదు ఎందుకంటే ఇది ప్రొడక్ట్స్ యొక్క అసలు లిస్ట్ను తీసుకొని, సెర్చ్ టెక్స్ట్ మరియు చెక్‌బాక్స్ వేల్యూ ప్రకారం ఫిల్టర్ చేయడం ద్వారా కంప్యూట్ చేయబడుతుంది**.

దీని అర్థం సెర్చ్ టెక్స్ట్ మరియు చెక్‌బాక్స్ వేల్యూ మాత్రమే state! చక్కగా చేసారు!

<DeepDive>

#### props వర్సెస్ state {/*props-vs-state*/}

React ‌లో రెండు రకాల "మోడల్" డేటా ఉన్నాయి: props మరియు state. రెండూ చాలా భిన్నమైనవి:

* [**props** మీరు ఒక ఫంక్షన్‌కు పంపే ఆర్గుమెంట్ల వంటివి](/learn/passing-props-to-a-component). అవి పేరెంట్ కాంపోనెంట్‌ నుండి చైల్డ్ కాంపోనెంట్‌కి డేటాను పాస్ చేయడానికి మరియు దాని అప్పీరెన్స్ ని కస్టమైజ్ చేసుకోవడానికి అనుమతిస్తాయి. ఉదాహరణకు, `Form` కాంపోనెంట్‌ `Button` కాంపోనెంట్‌ కి `color` prop ని పంపగలదు.
* [**state** అనేది కాంపోనెంట్ యొక్క జ్ఞాపకశక్తి లాంటిది](/learn/state-a-components-memory). ఇది కొంత సమాచారాన్ని ట్రాక్ చేయడానికి మరియు పరస్పర చర్యలకు ప్రతిస్పందనగా మార్చడానికి ఒక కాంపోనెంట్ని అనుమతిస్తుంది. ఉదాహరణకు, ఒక `Button` `isHovered` state ని ట్రాక్ చేయవచ్చు.

props మరియు state భిన్నంగా ఉంటాయి, కానీ అవి కలిసి పనిచేస్తాయి. ఒక పేరెంట్ కాంపోనెంట్ తరచుగా కొంత సమాచారాన్ని state లో ఉంచుతుంది (తద్వారా అది మార్చగలదు), మరియు *దాని చైల్డ్ కాంపోనెంట్‌లకు* వాటి props గా పంపుతుంది. ఒక్కసారి చదివినా తేడాలు ఇంకా అస్పష్టంగా ఉన్నా పర్వాలేదు. కొంచెం ప్రాక్టీస్‌తో మీరు సరిగ్గా అర్థం చేసుకోవచ్చు!

</DeepDive>

## స్టెప్ 4: మీ state ఎక్కడ నివసించాలో గుర్తించండి {/*step-4-identify-where-your-state-should-live*/}

మీ యాప్ యొక్క మినిమల్ state డేటాను గుర్తించిన తర్వాత, ఈ state ని మార్చడానికి ఏ కాంపోనెంట్ బాధ్యత వహిస్తుందో లేదా state ని *స్వంతం* చేసుకుంటుందో మీరు గుర్తించాలి. గుర్తుంచుకోండి: React వన్-వే డేటా ఫ్లోను ఉపయోగిస్తుంది, పేరెంట్ నుండి చైల్డ్ కాంపోనెంట్‌కు కాంపోనెంట్ హైరార్కి నుండి డేటాను పంపుతుంది. ఏ కాంపోనెంట్ ఏ state ని కలిగి ఉండాలో వెంటనే స్పష్టంగా తెలియకపోవచ్చు. మీరు ఈ కాన్సెప్ట్‌కు కొత్త అయితే ఇది సవాలుగా ఉంటుంది, కానీ మీరు ఈ స్టెప్స్ అనుసరించడం ద్వారా దాన్ని గుర్తించవచ్చు!

మీ అప్లికేషన్‌లోని ప్రతి state కోసం:

1. ఆ state ఆధారంగా ఏదైనా రెండర్ చేసే *ప్రతి* కాంపోనెంట్ని గుర్తించండి.
2. వారి అత్యంత క్లోసెస్ట్ కామన్ పేరెంట్ కాంపోనెంట్‌ను కనుగొనండి--హైరార్కి క్రమంలో అన్నింటి కంటే పైన ఉన్న కాంపోనెంట్.
3. state ఎక్కడ నివసించాలో నిర్ణయించండి:
    1. తరచుగా, మీరు state ని వారి కామన్ పేరెంట్స్కు డైరెక్ట్ గా ఉంచవచ్చు.
    2. మీరు state ని వారి కామన్ పేరెంట్ పైన కొంత కాంపోనెంటు గా కూడా ఉంచవచ్చు.
    3. మీరు state ని స్వంతం చేసుకోవడంలో అర్ధవంతమైన కాంపోనెంట్‌ను కనుగొనలేకపోతే, state ని హోల్డ్ చేసుకోవడం కోసం మాత్రమే కొత్త కాంపోనెంట్‌ని సృష్టించండి మరియు కామన్ పేరెంట్ కాంపోనెంట్ పైన ఉన్న హైరార్కిలో ఎక్కడో జోడించండి.

మునుపటి స్టెప్లో, మీరు ఈ అప్లికేషన్‌లో state కి సంబంధించిన రెండు కాంపోనెంట్లను కనుగొన్నారు: సెర్చ్ ఇన్‌పుట్ టెక్స్ట్ మరియు చెక్‌బాక్స్ వేల్యూ. ఈ ఉదాహరణలో, అవి ఎల్లప్పుడూ కలిసి కనిపిస్తాయి, కాబట్టి వాటిని ఒకే ప్లేసులో ఉంచడం అర్ధమే.

ఇప్పుడు వాటి కోసం మన వ్యూహాన్ని అమలు చేద్దాం:

1. **state ని ఉపయోగించే కాంపోనెంట్లను గుర్తించండి:**
    * `ProductTable` ఆ state (సెర్చ్ టెక్స్ట్ మరియు చెక్‌బాక్స్ వేల్యూ) ఆధారంగా ప్రోడక్ట్ లిస్ట్ను ఫిల్టర్ చేయాలి. 
    * `SearchBar` ఆ state ని ప్రదర్శించాలి (సెర్చ్ టెక్స్ట్ మరియు చెక్‌బాక్స్ వేల్యూ).
2. **వారి కామన్ పేరెంట్ను కనుగొనండి:** రెండు కాంపోనెంట్లు పంచుకునే మొదటి పేరెంట్ కాంపోనెంట్ `FilterableProductTable`.
3. **state ఎక్కడ నివసిస్తుందో నిర్ణయించండి**: మేము ఫిల్టర్ టెక్స్ట్ మరియు చెక్ చేసిన state వేల్యూలను `FilterableProductTable` లో ఉంచుతాము.

కాబట్టి state వేల్యూలు `FilterableProductTable` లో ఉంటాయి. 

[`useState() హుక్‌`](/reference/react/useState) తో కాంపోనెంట్‌కు state ను జోడించండి. హుక్స్ అనేవి మిమల్ని React కి "హుక్ ఇన్" చేసే ప్రత్యేక ఫంక్షన్స్. `FilterableProductTable` ఎగువన రెండు state వేరియబుల్‌లను జోడించి, వాటి ఇనీటియాల్ state ని పేర్కొనండి:

```js
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);  
```

ఆపై, `filterText` మరియు `inStockOnly` ని `ProductTable` మరియు `SearchBar` కి props గా పాస్ చేయండి:

```js
<div>
  <SearchBar 
    filterText={filterText} 
    inStockOnly={inStockOnly} />
  <ProductTable 
    products={products}
    filterText={filterText}
    inStockOnly={inStockOnly} />
</div>
```

మీ అప్లికేషన్ ఎలా ప్రవర్తిస్తుందో మీరు చూడటం ప్రారంభించవచ్చు. దిగువ శాండ్‌బాక్స్ కోడ్‌లో `filterText` ఇనీటియాల్ వేల్యూను `useState('')` నుండి `useState('fruit')` కి ఎడిట్ చేయండి. మీరు సెర్చ్ ఇన్‌పుట్ టెక్స్ట్ మరియు టేబుల్ అప్‌డేట్ రెండింటినీ చూస్తారు:

<Sandpack>

```jsx src/App.js
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} />
      <ProductTable 
        products={products}
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding-top: 5px;
}
td {
  padding: 2px;
}
```

</Sandpack>

ఫోర్మ్ను ఎడిట్ చేయడం ఇంకా పని చేయలేదని గమనించండి. పైన ఉన్న శాండ్‌బాక్స్‌లో కన్సోల్ ఎర్రర్ ఎందుకు ఉంది అని వివరిస్తుంది:

<ConsoleBlock level="error">

You provided a \`value\` prop to a form field without an \`onChange\` handler. This will render a read-only field.

</ConsoleBlock>

ఎగువ శాండ్‌బాక్స్‌లో, `ProductTable` మరియు `SearchBar` టేబుల్, ఇన్‌పుట్ మరియు చెక్‌బాక్స్‌ను రెండర్ చేయడానికి `filterText` మరియు `inStockOnly` prop లను చదవండి. ఉదాహరణకు, ఇన్‌పుట్ వేల్యూను `SearchBar` ఎలా పోపులేట్ చేస్తుందో ఇక్కడ ఉంది:

```js {1,6}
function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
```

అయినప్పటికీ, టైపింగ్ వంటి యూజర్ ఆక్షన్లకు రెస్పొంద్ అవ్వడానికి మీరు ఇంకా ఏ కోడ్‌ను జోడించలేదు. ఇది మీ చివరి దశ అవుతుంది.


## స్టెప్ 5: ఇన్వెర్సె డేటా ఫ్లో ని జోడించండి {/*step-5-add-inverse-data-flow*/}

ప్రస్తుతం మీ యాప్ props మరియు క్రిందికి ప్రవహించే హైరార్కి state తో సరిగ్గా అందించబడుతుంది. కానీ యూసర్ ఇన్‌పుట్ ప్రకారం state ని మార్చడానికి, మీరు ఇతర మార్గంలో ప్రవహించే డేటాకు సపోర్ట్ ఇవ్వాలి: హైరార్కి లో లోతైన ఫారమ్ కాంపోనెంట్లు `FilterableProductTable` లో state ని అప్డేట్ చేయాలి.

React ఈ డేటా ఫ్లో ని స్పష్టంగా చేస్తుంది, అయితే దీనికి రెండు-మార్గాల డేటా బైండింగ్ కంటే కొంచెం ఎక్కువ టైపింగ్ అవసరం. మీరు ఎగువ ఉదాహరణలో బాక్స్ను టైప్ చేయడానికి లేదా చెక్ చేయడానికి ప్రయత్నిస్తే, React మీ ఇన్‌పుట్‌ను ఇగ్నోర్ చేస్తుంది అని మీరు గమనిస్తారు. ఇది ఉద్దేశపూర్వకం. `<input value={filterText} />` ని వ్రాయడం ద్వారా, మీరు `input` యొక్క `value` prop ని ఎల్లప్పుడూ `FilterableProductTable` నుండి అందించిన `filterText` state కి సమానంగా ఉండేలా సెట్ చేసారు. `filterText` state ఎప్పుడూ సెట్ చేయబడనందున, ఇన్‌పుట్ ఎప్పటికీ మారదు.

యూసర్ ఫోర్మ్ ఇన్‌పుట్‌లను మార్చినప్పుడల్లా, ఆ మార్పులను రిఫ్లెక్ట్ చేసేలా state అప్డేట్ చేయబడుతుంది అని మీరు దీన్ని చేయాలనుకుంటున్నారు. state `FilterableProductTable` యాజమాన్యంలో ఉంది, కనుక ఇది మాత్రమే `setFilterText` మరియు `setInStockOnly` ని కాల్ చేయగలదు. `SearchBar` ని `FilterableProductTable` state ని అప్‌డేట్ చేయడానికి, మీరు ఈ ఫంక్షన్‌లను `SearchBar` కి పంపాలి:

```js {2,3,10,11}
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly}
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly} />
```

`SearchBar` లోపల, మీరు `onChange` ఈవెంట్ హ్యాండ్లర్‌లను జోడించి, వాటి నుండి పేరెంట్ state ని సెట్ చేస్తారు:

```js {4,5,13,19}
function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange
}) {
  return (
    <form>
      <input
        type="text"
        value={filterText}
        placeholder="Search..."
        onChange={(e) => onFilterTextChange(e.target.value)}
      />
      <label>
        <input
          type="checkbox"
          checked={inStockOnly}
          onChange={(e) => onInStockOnlyChange(e.target.checked)}
```

ఇప్పుడు అప్లికేషన్ పూర్తిగా పనిచేస్తుంది!

<Sandpack>

```jsx src/App.js
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} 
        onFilterTextChange={setFilterText} 
        onInStockOnlyChange={setInStockOnly} />
      <ProductTable 
        products={products} 
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange
}) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} placeholder="Search..." 
        onChange={(e) => onFilterTextChange(e.target.value)} />
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} 
          onChange={(e) => onInStockOnlyChange(e.target.checked)} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding: 4px;
}
td {
  padding: 2px;
}
```

</Sandpack>

మీరు ఈవెంట్‌లను హేండిల్ చేయడం మరియు state ని అప్డేట్ చేయడం గురించి [ఇంటరాక్టివిటీని జోడించడం](/learn/adding-interactivity) విభాగంలో తెలుసుకోవచ్చు.

## ఇక్కడి నుంచి ఎక్కడికి వెళ్లాలి {/*where-to-go-from-here*/}

React తో కాంపోనెంట్లను బిల్డ్ చేయడం మరియు అప్లికేషన్లను తయారు చేయడం గురించి ఎలా ఆలోచించాలో ఇది చాలా బ్రీఫ్ పరిచయం. మీరు ఇప్పుడే [React ప్రాజెక్ట్‌ను ప్రారంభించవచ్చు](/learn/installation) లేదా ఈ ట్యుటోరియల్‌లో ఉపయోగించిన [అన్ని సింటాక్స్‌పై లోతుగా డైవ్ చేయండి](/learn/describing-the-ui).
