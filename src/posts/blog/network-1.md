---
title: 'NETWORK | 0.Next.js를 공부하기 전에'
category: 'NETWORK'
date: '2023-07-05T15:17:00'
desc: 'Next.js, CSR, SSR, SPA'
thumbnail: './images/getting-started/thumbnail.jpg'
alt: 'Next.js, CSR, SSR, SPA'
---

## 1. CSR(Client-side Rendering)

- **정의**
  웹 페이지의 초기 요청에 대한 응답으로 HTML, CSS, Javascript 파일을 다운로드하여, 브라우저에서 Javascript 파일을 실행하여 웹 애플리케션을 로드하는 렌더링 방법

- **장점** 1. **사용자 경험** : CSR은 페이지가 로드된 후 사용자와 상호작용이 빠르게 이루어진다. 따라서 초기 로딩 시간 이후에는 사용자에게 더 나은 경험을 제공할 수 있다. 2. **서버 부담 감소** : CSR은 말 그대로 Client Side에서 모든 렌더링과 상호작용 로직이 실행된다. 따라서 서버의 부담을 줄일 수 있다. 3. **코드 재사용성** : CSR에서는 에서는 프론트엔드와 백엔드가 분리되어 작동한다. 프론트엔드는 클라이언트(브라우저)에서 실행되며, 백엔드는 서버에서 실행되는 구조는 재사용 가능한 코드를 생성하는데 도움을 준다.
- **단점** 1. **검색엔진 최적화(SEO)** : CSR의 정의에 기재한 바와 같이, 초기 요청에 대한 응답으로 HTML, CSS 및 JavaScript 파일을 다운로드를 하는 경우 HTML에는 초기 페이지의 콘텐츠가 포함되어 있지 않거나 매우 제한적으로 포함되어 있을 수 있다. 이때, 검색 엔진은 웹 페이지의 내용을 크롤링하여 색인화(Indexing : 검색 엔진이 웹 페이지를 이해하고 검색 결과에 포함시키기 위해 웹 페이지의 콘텐츠를 처리하는 과정)하는 경우, 해당 페이지의 콘텐츠가 검색 결과에 적절하게 나타나지 않을 수 있다. 2. **초기 로딩 시간** : 초기 Javascript 파일의 다운로드와 실행 시간이 소요됨에 따라 초기 페이지 로딩 시간이 길어질 수 있다. 느린 인터넷 연결 또는 느린 장치에서는 사용자 경험이 저하 될 수 있다.

## 2.SPA에서 SSR이 필요한 이유

- **SPA(Single Page Application) 정의**
  웹 애플리케이션의 디자인 패턴이다. 전체 페이지를 **새로고침**하지 않고 동적으로 컨텐츠를 업데이트한다. 약자 그대로, 초기에 한번 페이지를 로드하고, 이후에는 클라이언트 사이드에서 Javascript를 사용하여 필요한 데이터를 서버에 요청하고, 새로운 컨첸츠를 렌더링한다.

- **SSR(Server-Side Rendering) 정의**
  서버 사이드 렌더링이란, 서버에서 요청에 대한 응답으로 완전히 렌더링된 HTML을 제공하여 렌더링하는 것이다. 조금 더 풀어서 이야기하자면 서버에서 사용자에게 보여줄 페이지를 모두 미리 구성한 뒤 페이지를 렌더링하는 것이다. 이후 추가적인 상호작용은 클라이언트에서 JavaScript를 통해 실행할 수 있다.

- **SPA에서 SSR이 필요한 이유** 1. **검색엔진 최적화(SEO)** : 많은 수의 사용자를 대상으로 한다면, SEO 최적화를 위해서 SSR은 필수이다. 2. **사용자 경험** : SSR을 사용하면 초기 페이지의 빠른 로딩을 통해 사용자에게 빠른 응답성을 제공한다.

✔️ 다만, 렌더링 방식의 선택 기준은 서비스, 프로젝트, 컨텐츠의 성격에 따라 달라질 수 있다.

- SSR: 1)상위 노출, 2)누구에게나 동일한 내용 노출, 3)페이지마다 데이터가 자주 변경
- CSR : 1)개인정보 데이터 기준, 2)고객 데이터 보호, 3)보다 나은 사용자 경험 제공

## 3. Next.js 프로젝트에서 yarn start(or npm run start) 스크립트를 실행했을 때 실행되는 코드

```js
#!/usr/bin/env node

import arg from 'next/dist/compiled/arg/index.js';
import { startServer } from '../server/lib/start-server';
import { getPort, printAndExit } from '../server/lib/utils';
import isError from '../lib/is-error';
import { getProjectDir } from '../lib/get-project-dir';
import { CliCommand } from '../lib/commands';
import { resolve } from 'path';
import { PHASE_PRODUCTION_SERVER } from '../shared/lib/constants';
import loadConfig from '../server/config';

const nextStart: CliCommand = async (argv) => {
  const validArgs: arg.Spec = {
    // Types
    '--help': Boolean,
    '--port': Number,
    '--hostname': String,
    '--keepAliveTimeout': Number,

    // Aliases
    '-h': '--help',
    '-p': '--port',
    '-H': '--hostname',
  };
  let args: arg.Result<arg.Spec>;
  try {
    args = arg(validArgs, { argv });
  } catch (error) {
    if (isError(error) && error.code === 'ARG_UNKNOWN_OPTION') {
      return printAndExit(error.message, 1);
    }
    throw error;
  }
  if (args['--help']) {
    console.log(`
      Description
        Starts the application in production mode.
        The application should be compiled with \`next build\` first.

      Usage
        $ next start <dir> -p <port>

      <dir> represents the directory of the Next.js application.
      If no directory is provided, the current directory will be used.

      Options
        --port, -p          A port number on which to start the application
        --hostname, -H      Hostname on which to start the application (default: 0.0.0.0)
        --keepAliveTimeout  Max milliseconds to wait before closing inactive connections
        --help, -h          Displays this message
    `);
    process.exit(0);
  }

  const dir = getProjectDir(args._[0]);
  const host = args['--hostname'];
  const port = getPort(args);

  const keepAliveTimeoutArg: number | undefined = args['--keepAliveTimeout'];
  if (
    typeof keepAliveTimeoutArg !== 'undefined' &&
    (Number.isNaN(keepAliveTimeoutArg) ||
      !Number.isFinite(keepAliveTimeoutArg) ||
      keepAliveTimeoutArg < 0)
  ) {
    printAndExit(
      `Invalid --keepAliveTimeout, expected a non negative number but received "${keepAliveTimeoutArg}"`,
      1
    );
  }

  const keepAliveTimeout = keepAliveTimeoutArg
    ? Math.ceil(keepAliveTimeoutArg)
    : undefined;

  const config = await loadConfig(
    PHASE_PRODUCTION_SERVER,
    resolve(dir || '.'),
    undefined,
    undefined,
    true
  );

  await startServer({
    dir,
    isDev: false,
    hostname: host,
    port,
    keepAliveTimeout,
    useWorkers: !!config.experimental.appDir,
  });
};

export { nextStart };
```

> 출처
>
> - 실전 리액트 프로그래밍(개정판) (이재승 저), 서버사이드 렌더링 그리고 Next.js
> - [SSR(서버사이드 렌더링)과 CSR(클라이언트 사이드 렌더링)](https://miracleground.tistory.com/entry/SSR%EC%84%9C%EB%B2%84%EC%82%AC%EC%9D%B4%EB%93%9C-%EB%A0%8C%EB%8D%94%EB%A7%81%EA%B3%BC-CSR%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8-%EC%82%AC%EC%9D%B4%EB%93%9C-%EB%A0%8C%EB%8D%94%EB%A7%81)
> - [Next.js](https://github.dev/vercel/next.js/tree/canary/packages/next/src/server)
