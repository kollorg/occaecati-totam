# @kollorg/occaecati-totam
Declarative library for describing endpoints.

## Install

npm:
```sh
npm install @kollorg/occaecati-totam
```

yarn:
```sh
yarn add @kollorg/occaecati-totam
```

## Usage

Describe your request scheme

```js
import @kollorg/occaecati-totam from '@kollorg/occaecati-totam';

export const requests = @kollorg/occaecati-totam('10.16.0.140', 9001)
    .group('list', {
        get: {
            all: 'get-all-lists',
        },
        post: {
            save: 'save-list',
            create: 'get-empty-list'
        }
    })
    .group('ports', {
        get: {
            ports: (count) => `get-ports?count=${count}`,
        }
    })
    .end();
```

And send your requests to any place

```js
import { requests } from 'requests';

const showLists = async () => {
    try {
        const response = await fetch(requests.list.get.all);
        const answer = await response.json();
        console.log(answer);
    } catch (error) {
        console.error(error);
    }
}
```

```js
import { requests } from 'requests';
import axios from 'axios';

const showLists = async () => {
    try {
        const response = await axios.get(requests.list.get.all);
        console.log(response.data);
    } catch (error) {
        console.error(error);
    }
}
```

## License

[MIT](LICENSE)