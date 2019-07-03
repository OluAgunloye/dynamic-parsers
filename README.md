### Installation

```bash
npm install dynamic-parsers --save
```

<br>


# Multi-Platform Strings Files Manager

### Define Translations Data Structure
```js
const translations = [
  { key: 'HELLO', translations: { en: 'Hello English', fr: 'Hello French' }, platforms: ['ANDROID', 'IOS', 'WEB'] },
  { key: 'ERROR', translations: { en: 'Error English', fr: 'Error French' }, platforms: ['ANDROID', 'IOS', 'WEB'] },
  { key: 'EMAIL_INUSE', translations: { en: 'Email in use English', fr: 'Email in use French' }, platforms: ['ANDROID', 'IOS'] },
];
```

### Setup Generator
```js
const { StringsGenerator } = require('dynamic-parsers');

const generator = new StringsGenerator(translations, ['en', 'fr']);
```

### Option 1 - Write to a Local File
```js
// async/await
(async() => {

  const platform = 'ANDROID'; // 'IOS' || 'ANDROID' || 'WEB' || 'API'
  const zipFile = await generator.generateZip(platform);
  fs.writeFileSync('file.zip', zipFile);
  
})();


// Promise
generator.generateZip(platform).then(zipFile => {

  const platform = 'ANDROID'; // 'IOS' || 'ANDROID' || 'WEB' || 'API'
  fs.writeFileSync('file.zip', zipFile);

});
```

### Option 2 - Serve in API using a Simple Express Server
```js
app.get('/generator', async (req, res) => {

  const platform = 'ANDROID'; // 'IOS' || 'ANDROID' || 'WEB' || 'API'
  const zipFile = await generator.generateZip(platform);

  res.writeHead(200, {
    'Content-Type': 'application/zip',
    'Content-Length': zipFile.length
  });
  
  return res.end(zipFile);
});
```

### Class Parameters

``const generator = new StringsGenerator(translations, languages)``

|param|default|type
|---|---|---|
|translations|(required)|[Translations](#translations-interface)|
|languages|(required)|string[]|

### Translations Interface

```js
export type Platform = 'WEB' | 'ANDROID' | 'IOS' | 'API';

export interface Transalations {
  readonly translations: { [key: string]: string }; // e.g. { en: 'Good Morning', fr: 'Bonjour' }
  readonly translatable?: boolean;
  readonly platforms: Platform[];
  readonly key: string;
}
```

<br>

# Web Crawler and Scraper

### Keep in touch! Coming Soon!

<br>

#### Contact Author: [Serge Harb](mailto:me@sergeharb.com)