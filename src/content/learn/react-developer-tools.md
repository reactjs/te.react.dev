---
title: React డెవలపర్ టూల్స్
---

<Intro>

React [కాంపోనెంట్‌లను](/learn/your-first-component) తనిఖీ చేయడానికి, [props](/learn/passing-props-to-a-component) మరియు [state](/learn/state-a-components-memory) ని ఎడిట్ చేయడానికి మరియు పెర్ఫార్మన్స్ సమస్యలను గుర్తించడానికి React డెవలపర్ టూల్స్ ను ఉపయోగించండి.

</Intro>

<YouWillLearn>

* React డెవలపర్ టూల్స్ ను ఎలా ఇన్‌స్టాల్ చేయాలి

</YouWillLearn>

## బ్రౌజర్ ఎక్సటెన్షన్ {/*browser-extension*/}

React తో నిర్మించిన వెబ్‌సైట్‌లను డీబగ్ చేయడానికి సులభమైన మార్గం React డెవలపర్ టూల్స్ బ్రౌజర్ ఎక్సటెన్షన్ ను ఇన్‌స్టాల్ చేయడం. ఇది అనేక ప్రసిద్ధ బ్రౌజర్‌లకు అందుబాటులో ఉంది:

* [**Chrome** కోసం ఇన్‌స్టాల్ చేయండి](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
* [**Firefox** కోసం ఇన్‌స్టాల్ చేయండి](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
* [**Edge** కోసం ఇన్‌స్టాల్ చేయండి](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

ఇప్పుడు, మీరు **React తో నిర్మించిన వెబ్‌సైట్‌** ను సందర్శిస్తే, మీరు _Components_ మరియు _Profiler_ ప్యానెల్‌లను చూస్తారు.

![React డెవలపర్ టూల్స్ ఎక్స్టెన్షన్](/images/docs/react-devtools-extension.png)

### Safari మరియు ఇతర బ్రౌజర్‌లు {/*safari-and-other-browsers*/}
ఇతర బ్రౌజర్‌ల కోసం (ఉదాహరణకు, Safari), [`react-devtools`](https://www.npmjs.com/package/react-devtools) npm ప్యాకేజీని ఇన్‌స్టాల్ చేయండి:
```bash
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```

తరువాత టెర్మినల్ నుండి డెవలపర్ టూల్స్ ను ఓపెన్ చేయండి:
```bash
react-devtools
```

ఆపై మీ వెబ్‌సైట్ యొక్క `<head>` ప్రారంభంలో క్రింది `<script>` ట్యాగ్‌ని జోడించడం ద్వారా మీ వెబ్‌సైట్‌ను కనెక్ట్ చేయండి:
```html {3}
<html>
  <head>
    <script src="http://localhost:8097"></script>
```

ఇప్పుడు మీ బ్రౌజర్‌లో వెబ్‌సైట్‌ను రీలోడ్ చేయండి, తద్వారా మీరు దీన్ని డెవలపర్ టూల్స్ లో వీక్షించవచ్చు.

![React డెవలపర్ టూల్స్ స్టాండ్ అలొనె](/images/docs/react-devtools-standalone.png)

<<<<<<< HEAD
## మొబైల్ (React Native) {/*mobile-react-native*/}
[React Native](https://reactnative.dev/) తో రూపొందించబడిన యాప్‌లను తనిఖీ చేయడానికి కూడా  React డెవలపర్ టూల్స్ ను ఉపయోగించవచ్చు.

React డెవలపర్ టూల్స్ ను ఉపయోగించడానికి సులభమైన మార్గం దీన్ని గ్లోబల్గా ఇన్‌స్టాల్ చేయడం:
```bash
# Yarn
yarn global add react-devtools
=======
## Mobile (React Native) {/*mobile-react-native*/}

To inspect apps built with [React Native](https://reactnative.dev/), you can use [React Native DevTools](https://reactnative.dev/docs/debugging/react-native-devtools), the built-in debugger that deeply integrates React Developer Tools. All features work identically to the browser extension, including native element highlighting and selection.
>>>>>>> 3b02f828ff2a4f9d2846f077e442b8a405e2eb04

[Learn more about debugging in React Native.](https://reactnative.dev/docs/debugging)

<<<<<<< HEAD
తరువాత టెర్మినల్ నుండి డెవలపర్ టూల్స్ ను ఓపెన్ చేయండి.
```bash
react-devtools
```

దీన్ని రన్నింగ్లో ఉన్న ఏదైనా లోకల్ React Native యాప్‌కి కనెక్ట్ చేయాలి.

> డెవలపర్ టూల్స్ కొన్ని సెకన్ల తర్వాత కనెక్ట్ కాకపోతే యాప్‌ని రీలోడ్ చేయడానికి ప్రయత్నించండి.

[React Native డీబగ్గింగ్ గురించి మరింత తెలుసుకోండి.](https://reactnative.dev/docs/debugging)
=======
> For versions of React Native earlier than 0.76, please use the standalone build of React DevTools by following the [Safari and other browsers](#safari-and-other-browsers) guide above.
>>>>>>> 3b02f828ff2a4f9d2846f077e442b8a405e2eb04
