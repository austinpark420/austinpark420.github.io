---
layout: post
title: async/await에 대해서
permalink: posts/async&await
tag: [javascript, ECMAScript]
---

> 해당 포스트는 [How To Master Async/Await With This Real World Example](https://medium.freecodecamp.org/how-to-master-async-await-with-this-real-world-example-19107e7558ad)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

1. callbacks, promises, async/await 소개
2. 사용 예시 - 환율계산기, 2개의 API로 비동기로 데이터 전달받기

<<<<<<< HEAD
필자는 해당 아티클과 함께 유튜브 동영상도 함께 제작했습니다. 글을 먼저 읽고 유튜브를 보는 것을 추천드립니다.
=======
필자는 해당 아티클과 함께 유튜브 동영상도 함께 제작했습니다. 글을 먼저 읽고 유튜브를 보는 것을 추천해 드립니다.  
>>>>>>> 08f9a54f67295ea192e973146a006107d34a807e
[유튜브 바로가기](https://www.youtube.com/watch?v=mlb525FgU3k)

## 소개

Async/await는 비동기 코드를 작성하는 새로운 방법입니다. promises를 기반으로 설계되었기 때문에 논 블럭입니다.

async 코드의 장점은 보기에도 동기 코드와 같이 보이고 동기 코드와 같이 행동합니다. 이것이 Async/await의 이점입니다.

우선 callbacks과 promises를 살펴봅시다.

### callback

```javascript
setTimeout(() => {
  console.log("This run after 1000 milliseconds.");
}, 1000);
```

### callback 함수의 문제점 - 콜백헬

```javascript
  asyncCallOne(() => {
    asyncCallTwo(() => {
      asyncCallThree(() => {
        asyncCallFour(() => {
          asyncCallFive(() => {
            // ...
          }
        }
      }
    }
  })
```

### 콜백헬

이런한 현상은 콜백 함수가 다른 콜백 함수에 중첩되고 그 깊이가 깊어질 때 발생합니다. 잠정적으로 코드를 읽기 어렵게하고 유지하기 힘들게 합니다.

### Promise

```javascript
const promiseFunction = new Promise((resolve, reject) => {
  const add = (a, b) => a + b;
  resolve(add(2, 2));
});

promiseFunction
  .then(response => {
    console.log(response);
  })
  .catch(error => {
    console.log(error);
  });
```

promiseFunction은 해당 함수에서 프로세스를 나타내는 promise를 반환합니다. resolve 함수는 Promise 인스턴스가 끝났다는 신호입니다.

그 후에 우리는 then()과 catch()를 promise 함수에서 호출 할 수 있습니다.
then: promise가 종료된디 실행할 콜백함수를 전달합니다.
catch: 오류가 발생한 후에 실행할 콜백함수를 전달합니다.

### Async 함수

Async 함수는 깔끔하고 간결한 문법을 제공합니다. 이것은 우리가 promise를 사용해서 얻은 결과물과 동일한 값을 산출하는데 promise 보다 더 적은 양의 코드로 동일한 기능을 만들 수 있습니다.
Async 함수는 promise 문법적 설탕을 추가한 것 그 이상도 이하도 아닙니다.

Async 함수는 아래와 같이 함수 선언전에 async 키워드로 생성됩니다.

```javascript
const asyncFunction = async () => {
  // code
};
```

비동기 함수는 await으로 일시정지 시킬 수 있습니다. await는 async 함수 내부에서만 사용할 수 있습니다. await가 종료되었을 때 무엇이든 비동기 함수를 리턴할 수 있습니다.

promise와 async/await의 차이점은 아래와 같습니다.

```javascript
// async/await
const asyncGreeting = async () => "Greetings";

// promise
const promiseGreeting = () =>
  new Promise(resolve => {
    resolve("Greetings");
  });

asyncGreeting().then(result => console.log(result));
promiseGreeting().then(result => console.log(result));
```

async/await는 동기함수처럼 보이고 이해하기 쉽습니다.

그러면 기본적인 것에 대해서 좀더 알아 봅시다.

## 환율계산기

### 프로젝트 설명과 준비

튜토리얼에서 우리는 간단한 샘플을 만들지만 async/await에 대해서 배울 수 있는 교육적이고 유용한 어플리케이션을 만들 예정입니다.

이 프로그램은 우리가 변환하고 싶은 환율 코드와 현재 코드를 가지고 금액을 변환합니다. 그 후에 프로그램은 API를 통해 정확한 비율금액을 산출합니다.

어플리케이션 안에서 2개의 비동기 소스를 전달받을 예정입니다.

1. currency layer(https://currencylayer.com): API 접근 키를 발급 받기 위해서는 해당 사이트에 가입할 필요가 있습니다. 이 API는 환율을 계산하기에 필요한 환율 데이터를 제공합니다.

2. Rest Countires(http://restcountries.eu/): 이 API는 방금 변환한 금액을 어디서 사용할 수 있는지에 대한 정보를 제공합니다.

예를 들어, 새로운 디렉토리를 만들고 npm init을 실행하고 axios를 `npm i --save axios`으로 install합니다. 그리고`currency-converter.js`라는 파일을 생성합니다.

마지막으로 `const axios = require('axios')`으로 요청합니다.

### async/await에 대해서 알아 봅시다.

이 어플리케이션에서 우리의 목표는 3가지 함수를 가지는 것 입니다. 3개의 비동기 함수가 필요합니다. 첫 번째 함수는 환율을 패치하는 것이고, 두 번째 함수는 국가에 대한 정보를 가지고 오는 것이고, 세 번째 함수는 정보를 한곳에 모아서 유저에서 멋지게 보여주는 것 입니다.

### 첫 번째 함수 = 비동기로 환율 데이터 받아오기

우리는 환율을 계산할 2개의 통화를 인수로 전달받은 비동기함수를 만들예정입니다.

```javascript
const getExchangeRate = async (fromCurrency, toCurrency) => {};
```

우리는 데이터를 배치받아야 합니다. async/await를 활용해서 변수에 바로 데이터를 할당할 수 있습니다. 회원가입을하고 엑세스키를 발급받는 것을 잊으면 안됩니다!

```javascript
const getExchangeRate = async (fromCurrency, toCurrency) => {
  const response = await axios.get(
    "http://data.fixer.io/api/latest?access_key=[yourAccessky]&format=1"
  );
};
```

응답받은 데이터는 response.data.rates으로 사용할 수 있기 때문에 변수를 아래와 같이 설정할 수 있습니다.

```javascript
const rate = response.data.rates;
```

아래와 같이 모든 값들은 유로로 변환해야하기 때문에 유로 변수를 만들고 아래와 같이 할당합니다.

```javascript
const euro = 1 / rate[fromCurrency];
```

마지막으로 우리가 변환하고 싶은 환율을 구하기위해서 변환하려고 하는 통화에 유로를 곱할 수 있습니다.

```javascript
const exchangeRate = euro * rate[toCurrency];
```

마지마그로 함수는 아래와 같습니다.

```javascript
const getExchangeRate = async (fromCurrency, toCurrency) => {
  const response = await axios.get(
    "http://data.fixer.io/api/latest?access_key=[yourAccessky]&format=1"
  );

  const rate = response.data.rates;
  const euro = 1 / rate[fromCurrency];
  const exchangeRate = euro * rate[toCurrency];

  return exchangeRate;
};
```

### 두 번째 함수 - 비동기로 국가 데이터 받아오기

우리는 인수로 국가 코드를 받아오는 함수를 만들 예정입니다.

```javascript
const getCountries = async currencyCode => {};
```

이전과 같이 데이터를 패치받고 변수에 할당을 합니다.

```javascript
const response = await axios.get(
  `https://restconuntries.eu/rest/v2/currency/${currencyCode}`
);
```

우리는 데이터를 매핑해서 conutry.name을 각각 리턴합니다.

```javascript
return response.data.map(country => country.name);
```

두 번째 함수는 아래와 같습니다.

```javascript
const getCountries = async currencyCode => {
  const response = await axios.get(
    `https://restconuntries.eu/rest/v2/currency/${currencyCode}`
  );
  return response.data.map(country => country.name);
};
```

### 세 번째 함수 - 모든 것을 합치기

우리는 fromCurrency와 toCurrency, 금액을 취하는 비동기함수를 만들 예정입니다.

```javascript
const convert = async (fromCurrency, toCurrency, amount) => {};
```

먼저 현재 환율 데이터를 얻습니다.

```javascript
const exchangeRate = await getExchangeRate(fromCurrency, toCurrency);
```

두 번쩨, 국가에 대한 정보를 얻습니다.

```javascript
const countries = await getCountries(toCurrency);
```

세 번째, 변수에 변환된 값을 저장합니다.

```javascript
const converedAmount = (amount * exchangeRate).toFixed(2);
```

마지막으로 산출된 금액을 유저에게 전달합니다.

```javascript
return `${amount} ${fromCurrency} is worth ${convertedAmount} ${toCurrency}. You can spend these in the following countries: ${countries}`;
```

다 합쳐서 보면 아래와 같습니다.

```javascript
const convert = async (fromCurrency, toCurrency, amount) => {
  const exchangeRate = await getExchangeRate(fromCurrency, toCurrency);
  const countries = await getCountries(toCurrency);
  const converedAmount = (amount * exchangeRate).toFixed(2);

  return `${amount} ${fromCurrency} is worth ${convertedAmount} ${toCurrency}. You can spend these in the following countries: ${countries}`;
};
```

## 에러를 캐치하기위해서 try/catch를 추가하기

기존의 로직을 try으로 감싸고, 에러가 있다면 에러를 캐치합니다.

```javascript
const getExchangeRate = async (fromCurrency, toCurrency) => {
  try {
    const response = await axios.get(
      "http://data.fixer.io/api/latest?access_key=f68b13604ac8e570a00f7d8fe7f25e1b&format=1"
    );
    const rate = response.data.rates;
    const euro = 1 / rate[fromCurrency];
    const exchangeRate = euro * rate[toCurrency];
    return exchangeRate;
  } catch (error) {
    throw new Error(
      `Unable to get currency ${fromCurrency} and  ${toCurrency}`
    );
  }
};
```

두 번째 함수에도 동일한 작업을 반복합니다.

```javascript
const getCountries = async currencyCode => {
  try {
    const response = await axios.get(
      `https://restcountries.eu/rest/v2/currency/${currencyCode}`
    );
    return response.data.map(country => country.name);
  } catch (error) {
    throw new Error(`Unable to get countries that use ${currencyCode}`);
  }
};
```

첫 번째와 두 번째 함수 덕분에 세 번째 함수는 에러를 체크할 필요가 없습니다.

마지막으로 함수를 호출하고 데이터를 전달 받습니다.

```javascript
convertCurrency("USD", "HRK", 20)
  .then(message => {
    console.log(message);
  })
  .catch(error => {
    console.log(error.message);
  });
```

아래와 같은 같은 결과 값을 반환받습니다.
`20 USD is worth 129.90 HRK. You can spend these in the following countries: Croatia`

## 마무리

끝까지 다 만들었습니다. 만약 학습을 하다가 막히는 부분이 있다면 걱정하기말고 이 [레포](https://github.com/adrianhajdin/tutorial_currency_converter)를 참고하세요. 좀 더 도움이되는 내용은 [유튜브 채널](https://www.youtube.com/channel/UCmXmlB4-HJytD7wek0Uo97A?sub_confirmation=1)에서 확인이 가능합니다.
