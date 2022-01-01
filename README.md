# yarn-berry-workspace
yarn berry를 이용하여 workspace 구성해보기

## Set yarn berry
yarn을 기본적으로 설치하게 된다면 `1.x` 버전으로 설치가 됩니다. yarn berry를 사용하기 위해선 따로 버전을 설정해주어야 합니다.

1. Install yarn
    ```
    npm i -g yarn
    yarn -v // 1.x.x
    ```
1. Set yarn berry
    ```
    yarn set version berry
    yarn -v // 3.x.x
    ```

위와 같이 명령어로 yarn 버전을 변경할 수 있고 `.yarnrc.yml` 파일과 `.yarn` 폴더가 생성이 됩니다.
`.yarnrc.yml` yarn의 릴리즈 경로를 가르키고, `.yarn/releases/yarn-${version}.cjs` 파일은 yarn berry를 나타내는 것 같습니다.(추측)

## Initialize yarn berry
yarn을 berry로 설정했으니 초기화하고 종속성에 대해 설치를 진행합니다.

```
yarn init
yarn
```

<details>
<summary>VSCode assistant</summary>
<div>
zip 아카이브에 접근하기 위해서는 vscode sdk를 설치하고 extension을 설치해야 합니다.

```
yarn dlx @yarnpkg/sdk vscode
```

Extension [ZipFx](https://marketplace.visualstudio.com/items?itemName=arcanis.vscode-zipfs)
</div>
</details>
<br>

초기 구성이 된 후에 파일 경로는 아래와 같습니다.

```
├ .yarn
    ├ cache
        ⌊ .gitignore
    ├ releases
        ⌊ yarn-3.1.0.cjs
    ⌊ install-state.gz
├ .pnp.cjs
├ .yarnrc.yml
```

[.gitignore가 필요한 파일](https://yarnpkg.com/getting-started/qa#which-files-should-be-gitignored)

- .yarn
    - `cache/*` 설치된 패키지들이 zip 아카이브로 설치되는 위치입니다.
    - `releases/*` 프로젝트에서 사용되는 릴리즈 정보를 포함합니다.
    - `install-state.gz` 최적화 파일입니다. 프로젝트의 상태에 대한 정보를 가지고 있습니다.
- `.pnp.cjs` 패키지들의 의존성 정보를 담고 있는 핵심 파일입니다. 
- `.yarnrc.yml` 프로젝트의 구성 파일입니다.

## Workspace
workspace를 사용하고 싶다면 `init` 명령어 뒤에 `-w` 옵션을 붙여줍니다.

```
yarn init -w
```

`package.json`에 private과 workspace 속성이 추가가 됩니다. workspace의 루트 폴더는 기본으로 `packages`라고 생기게 됩니다.

## 패키지 생성
패키지를 추가하기 위해서 `package.json` 파일에서 `workspace`로 지정된 폴더에 패키지 폴더를 생성합니다.

## 패키지 의존성

## 유용한 플러그인
`yarn workspaces` CLI를 사용하기 위해 [플러그인](https://yarnpkg.com/cli/workspaces/foreach)을 설치합니다.

```
yarn plugin import workspace-tools
```

여러 워크스페이스에 있는 스크립트를 동시에 실행시키기 위하여 사용할 수 있습니다.
```
yarn workspace foreach {commandName}
```
