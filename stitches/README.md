# Setting

```sh
# Short way
npx create-next-app --example with-stitches
```

> If you want to add the settings of stitches to cna project, check [this link](https://stitches.dev/blog/using-nextjs-with-stitches)

## Packages

```sh
yarn add @stitches/react
```

## Basic process

- [x] Add Configure file : `stitches.config.ts`
- [x] Add SSR settings in `_document.tsx`

> 이하 한글로 작성. 원문은 [해당 링크](https://stitches.dev/docs/installation) 확인

## SSR

`getCssText` 함수를 통해 가능

- 해당 함수는 SSR에서 필요한 CSS를 전달함
- 보다 나은 SSR을 위해 `style` 태그에 `id="stitches"` 를 전달하는 것을 권장

# Styling

## Object syntax(객체 구문)

번들 사이즈를 최소화하기 위해, 문자열 구문이 아닌 **객체 구문**을 유지합니다.
아래 예시들을 통해 이를 확인할 수 있습니다.

## Global styles(전역 스타일)

전역 스타일 초기화는 **`globalCss` 함수**를 통해 가능하다.
이는 앱에서 실행하는 새로운 함수를 반환한다.

- `_app` 페이지와 개별 페이지 동시에 반영 가능
  - `_app` 보다 개별 페이지 `globalCss` 가 우선
- `_document` 페이지 내 `globalCss` 는 미반영

## Basic usages(기본 사용법)

- 기본적으로 `emotion` 및 `styled-components` 와 흡사 (방식 생략)
- 추가적으로 다룰 수 있는 기능들만을 작성

```tsx
// stitches
const Button = styled("button", {
  backgroundColor: "gainsboro",
  borderRadius: "9999px",
  fontSize: "13px",
  border: "0",
});
```

```tsx
// emotion and styled-components
const Button = styled.button`
  backgroundcolor: gainsboro;
  borderradius: 9999px;
  fontsize: 13px;
  border: 0;
`;
```

- 위 작성 방식을 확인해보면 **객체 형식**으로 작성된 것을 확인할 수 있음
  - 문자열 구문을 채택하는 타 라이브러리와 구분됨을 확인 가능

## Target a Stitches component(Stitches 컴포넌트 지정)

```tsx
const Icon = styled("svg", {
  display: "inline-block",
  marginLeft: "5px",
  width: "16px",
});

const Button = styled("button", {
  // base styles

  [`& ${Icon}`]: {
    marginLeft: "5px",
  },
});

() => (
  <Button>
    Button
    <Icon>...</Icon>
  </Button>
);
```

## Target a React component(리액트 컴포넌트 지정)

- `toString` 메서드를 활용하여 추가 가능
  - 의도한 셀렉터와 매칭하기 위해 필요

```tsx
const RightArrow = () => (
  <svg className="right-arrow" ... />
);

// add a `toString` method
RightArrow.toString = () => '.right-arrow';

const Button = styled('button', {
  // base styles

  [`& ${RightArrow}`]: {
    display: 'inline-block',
    marginLeft: '5px',
    width: '16px',
  },
});

() => <Button>Button <RightArrow /></Button>;
```

## Import rules(`@import`)

- `globalCss` 에서 사용 가능

```tsx
const globalStyles = globalCss({
  "@import": "custom.css", // single
  "@import": ["custom1.css", "custom2.css"], // multiple
});
```

## Font face rules(`@font-face`)

- `globalCss` 에서 사용 가능

```tsx
const globalStyles = globalCss({
  // single
  "@font-face": {
    fontFamily: "CustomFont",
    src: 'local("CustomFont"), url("CustomFont.woff2")',
  },

  // multiple
  "@font-face": [
    {
      fontFamily: "CustomFont1",
      src: 'local("CustomFont1"), url("CustomFont1.woff2")',
    },
    {
      fontFamily: "CustomFont2",
      src: 'local("CustomFont2"), url("CustomFont2.woff2")',
    },
  ],
});
```

## Supports rules(`@supports`)

- `globalCss`, `styled`, `css` 에서 사용 가능

```tsx
const globalStyles = globalCss({
  "@supports (display: grid)": {
    body: {
      display: grid,
    },
  },
});

const Grid = styled("div", {
  "@supports (display: grid)": {
    display: grid,
  },
});
```

## Token aware values(토큰 사용)

- 속성과 토큰을 매핑하여 `$` 접두사를 통해 토큰 값을 사용할 수 있음

```tsx
import { createStitches } from "@stitches/react";

const { styled } = createStitches({
  theme: {
    colors: {
      blue: "royalblue",
    },
  },
});

const Button = styled("button", {
  backgroundColor: "$blue",
});
```

## Token aware values(토큰 사용)

- 속성과 토큰을 매핑하여 `$` 접두사를 통해 토큰 값을 사용할 수 있음
- 지역 스코프로 지정 가능
- 스케일 접두사로도 지정 가능

```tsx
import { createStitches } from "@stitches/react";

const { styled } = createStitches({
  theme: {
    colors: {
      blue: "royalblue",
    },
  },
});

const Button = styled("button", {
  backgroundColor: "$blue",

  // 지역 스코프
  $$shadow: "blueviolet",
  boxShadow: "0 0 0 3px $$shadow",

  // 스케일 접두사 지정
  marginTop: "$sizes$1",

  // 지역 스코프 + 스케일 접두사 지정
  $$shadowColor: "$colors$purple500",
  boxShadow: "0 0 0 15px $$shadowColor",
});
```

## Theme specific styles(테마별 스타일)

- 동적으로 생성된 테마별로 스타일링 가능
- 테마는 클래스명을 반환하기에 `.` 접두사를 꼭 붙여서 사용

```tsx
import { createStitches } from "@stitches/react";

const { styled, createTheme } = createStitches({
  theme: {},
});

const myTheme = createTheme({});

const Button = styled("button", {
  borderRadius: "9999px",
  fontSize: "13px",
  border: "0",

  [`.${myTheme} &`]: {
    backgroundColor: "$blue",
  },
});

() => (
  <div className={myTheme}>
    <Button>Button</Button>
  </div>
);
```

# Variants ("분기" 쯤으로 해석)

`variants` 라는 키 값을 통해 분기별 CSS를 지정할 수 있습니다.

```tsx
const Button = styled("button", {
  // base styles

  variants: {
    color: {
      violet: {
        backgroundColor: "blueviolet",
        color: "white",
        "&:hover": {
          backgroundColor: "darkviolet",
        },
      },
      gray: {
        backgroundColor: "gainsboro",
        "&:hover": {
          backgroundColor: "lightgray",
        },
      },
    },
  },
});

() => <Button color="violet">Button</Button>;
```

## Multiple variants(복수 분기)

```tsx
const Button = styled("button", {
  // base styles

  variants: {
    color: {
      violet: { ...violetStyles },
      gray: { ...grayStyles },
    },
    size: {
      small: {
        fontSize: "13px",
        height: "25px",
        paddingRight: "10px",
        paddingLeft: "10px",
      },
      large: {
        fontSize: "15px",
        height: "35px",
        paddingLeft: "15px",
        paddingRight: "15px",
      },
    },
  },
});

() => (
  <Button color="violet" size="large">
    Button
  </Button>
);
```

## Boolean variants(불리언 분기)

- `true` 키를 통해 `Boolean` 값 핸들링 가능

```tsx
const Button = styled("button", {
  // base styles

  variants: {
    outlined: {
      true: {
        borderColor: "lightgray",
      },
    },
  },
});

() => <Button outlined>Button</Button>;
```

## Compound variants(분기 내 스타일 합성)

- 다른 조합을 기반으로 해당 조합의 스타일링을 설정해야 할 때, `compoundVariants` 를 사용하여 가능

```tsx
const Button = styled("button", {
  ...styles,

  variants: {
    color: {
      violet: { ...violetStyles },
      gray: { ...grayStyles },
    },
    outlined: {
      true: { ...outlineVariants },
    },
  },

  compoundVariants: [
    {
      color: "violet",
      outlined: true,
      css: {
        color: "blueviolet",
        borderColor: "darkviolet",
        "&:hover": {
          color: "white",
        },
      },
    },
    {
      color: "gray",
      outlined: true,
      css: {
        color: "gray",
        borderColor: "lightgray",
        "&:hover": {
          color: "black",
        },
      },
    },
  ],
});

() => (
  <Button color="violet" outlined>
    Button
  </Button>
);
```

## Default variants(기본 분기)

- `defaultVariants` 를 통해 기본 `variants` 설정 가능

```tsx
const Button = styled('button', {
  ...styles

  variants: {
    color: {
      violet: { ...violetStyles },
      gray: { ...grayStyles }
    },
  },

  defaultVariants: {
    color: 'violet'
  }
});

() => <Button>Button</Button>
```

## Responsive variants(반응형 분기)

- 다양한 `breakpoints` 마다 `variants` 를 설정할 수도 있음
- `@initial` 을 통해 기본 `variants` 를 설정해주어야 한다.

```tsx
const Button = styled("button", {
  // base styles

  variants: {
    color: {
      violet: { ...violetStyles },
      gray: { ...grayStyles },
    },
  },
});

() => (
  <Button
    color={{
      "@initial": "gray",
      "@bp1": "violet",
    }}
  >
    Button
  </Button>
);
```

# Responsive

`createStitches` 내 `media` 키로 정의 가능

```ts
export const { styled, css } = createStitches({
  media: {
    bp1: "(min-width: 640px)",
    bp2: "(min-width: 768px)",
    bp3: "(min-width: 1024px)",
  },
});
```

## Using breakpoints in the style objects(스타일 객체에서 반응형 설정)

```tsx
const Button = styled("button", {
  // base styles

  "@bp1": {
    // Styles for bp1
  },
});
```

# Overriding Styles

`css` prop를 통해 스타일 오버라이드 가능

## The `css` prop

- 모든 Stitches 컴포넌트는 `css` prop을 가지며, 이를 통해 오버라이드 가능
- tokens, media queries, nesting, token-aware values 모두 사용 가능

```tsx
const Button = styled("button", {});

() => (
  <Button
    css={{
      borderRadius: "0",
      "&:hover": {
        backgroundColor: "black",
        color: "white",
      },
    }}
  >
    Button
  </Button>
);
```

## Merging css prop on custom components(커스텀 컴포넌트에 css prop 병합)

- `css` prop을 아래와 같이 병합 가능

```tsx
const PageTitle = styled("h1", {});

function BlogTitle({ css, ...props }) {
  return (
    <PageTitle
      css={{
        ...css,
        "@bp1": {
          ...css["@bp1"],
          lineHeight: 1.2,
        },
        "@bp2": {
          ...css["@bp2"],
          lineHeight: 1.4,
        },
      }}
      {...props}
    />
  );
}

() => (
  <BlogTitle
    css={{
      marginBottom: 10,
      "@bp1": { marginBottom: 20 },
      "@bp2": { marginBottom: 30 },
    }}
  >
    Blog title
  </BlogTitle>
);
```

## Overriding the HTML tag(HTML 오버라이드)

- `as` prop을 통해 HTML 오버라이드 가능

```tsx
const Button = styled("button", {});

() => (
  <Button as="a" href="#">
    Button
  </Button>
);
```

# Framework Agnostic Core API

> 프레임워크에 구애 받지 않는 방식이라고 함. React를 사용할 예정이기에 이는 제외
> 확인을 원한다면 [다음 링크](https://stitches.dev/docs/framework-agnostic)로

# Theme tokens(테마 토큰)

> 앞에서 사용했던 토큰에 대한 내용. 속성 매핑과 관련된 내용은 [다음 링크](https://stitches.dev/docs/tokens)로

# Utils

여러가지 유틸을 추가하여 효과적으로 스타일링 가능

```tsx
export const { styled, css } = createStitches({
  utils: {
    // A property for applying width/height together
    size: (value) => ({
      width: value,
      height: value,
    }),

    // A property to apply linear gradient
    linearGradient: (value) => ({
      backgroundImage: `linear-gradient(${value})`,
    }),

    // An abbreviated property for border-radius
    br: (value) => ({
      borderRadius: value,
    }),
  },
});
```

```tsx
const Box = styled("div", {
  size: "200px",
  linearGradient: "19deg, #21D4FD 0%, #B721FF 100%",
  br: "$round",
});
```
