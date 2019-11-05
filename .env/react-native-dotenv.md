

react-native-dotenv 는 개발환경과 프로덕현 환경을 구분하여 다른 변수를 사용할 수 있게 해주는 라이브러리입니다.

다른 라이브러리와는 다르게 js core에서 동작하기 때문에 적용하기가 간단하지만, 더 세분화된 세팅(android와 ios의 구분이라던가)를 할 수는 없습니다.

1. 설치

```
npm install metro-react-native-babel-preset --save-dev
npm install react-native-dotenv --save-dev
```

우선 babel-preset으로 js 코드가 마운트 될 때의 설정 파일 babel.config.js를 생성해 줍니다.

```
{
  module.exports = 
  {
    presets: ['module:metro-react-native-babel-preset'],
  };
}
```

처음의 내용은 이렇습니다.

```
module.exports = {
  presets: ['module:metro-react-native-babel-preset', "module:react-native-dotenv"],
};

```

이를 이상으로 변경합니다.

2. 활용

프로젝트의 root에 .env 와 .env.production을 생성합니다.

```
GODO_API_URL= `https://randomurl.api`
DJANGO_API_URL=`https://randomurldjango.api`
version=debug
```

각 파일에 필요한 변수들을 지정해 줍니다.

```
import {version} from 'react-native-dotenv'
```

설정된 변수들은 이런 형태로 불러올 수 있습니다.

