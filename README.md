<h1 align="center">Why we use stitches? ๐ค</h1>

> ๋์์ธ์์คํ์ stitches ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ ์ฉํ๊ธฐ ์ํ ํ๋น์ฑ์ ํ๋ณดํ๊ณ , ๋ณ๊ฒฝ์ด ๋ถํ์ํ๋ค๋ ์ด์  ๋ํ ๋์ถํ์ฌ ๊ณผํฌ์๋ฅผ ๋ฐฉ์งํ๊ณ ์ ํฉ๋๋ค.
> ์์ฑ ์ฌํญ์ ์ค๋ฅ๊ฐ ์๊ฑฐ๋, ์ด์ ๋ํ ์๊ฒฌ๊ณผ ๊ฐ์ ์ฌํญ๋ค์ ํ์ํฉ๋๋ค.

<br/>

# Environment

| Package           | Version |
| ----------------- | ------- |
| stitches          | 1.2.8   |
| @emotion/react    | 11.10.5 |
| styled-components | 5.3.6   |

# Differences

> ๊ฐ์ธ์ ์ผ๋ก ๋๋ ์ฐจ์ด์ ๋ํด ๊ธฐ์ ํฉ๋๋ค. ๋ค์ ๊ฐ๊ด์ ์ด์ง ์์ ์ ์์ต๋๋ค.
>
> - ๋ค์ ์ต์ํ์ง ์์ stitches์ ์ธ๋ถ ์ค๋ช์ด ํฌํจ๋๊ธฐ์ ์๋์ ์ผ๋ก stitches์ ๋ํ ๊ธฐ์ ์ด ๋ง์ ์ ์์ต๋๋ค.
> - Emotion๊ณผ Styled components๊ฐ ๋ค์ ์ ์ฌํ ์ ์ ๊ณ ๋ คํ์ฌ ๊ณต๋์ผ๋ก ์์ฑ๋๋ ๋ถ๋ถ์ด ๋ง์ต๋๋ค.
> - ๋๋๋ก ๊ณต์ ๋ฌธ์๋ฅผ ๊ธฐ์ค์ผ๋ก ํ์ผ๋ฉฐ, ์ถ๊ฐ์ ์ธ ๋ฐฉ๋ฒ๋ก ๋ค์ ๋ ํผ๋ฐ์ค๋ฅผ ํตํด ์ฐธ๊ณ ํ์ต๋๋ค.

## Syntax

> ์ ๋ฐ์ ์ธ ์คํ์ผ๋ง ์ฝ๋ ์์ฑ ๋ฐฉ์ ์ฐจ์ด๋ฅผ ์์ฝํ์ฌ ๊ธฐ์ ํ์ต๋๋ค.

### stitches

๊ฐ์ฒด ํํ์ ์์ฑ ๋ฐฉ์์ ์ฑํํฉ๋๋ค.

- ๋ฒ๋ค ์ฌ์ด์ฆ๋ฅผ ์ต์ํ ํ๊ธฐ ์ํจ์ด๋ผ๊ณ  ํฉ๋๋ค.

```ts
const Button = styled("button", {
  backgroundColor: "gainsboro",
  borderRadius: "9999px",
  fontSize: "13px",
  border: "0",
});
```

### emotion & styled

๋ฌธ์์ด ์์ฑ ๋ฐฉ์๊ณผ ๊ฐ์ฒด ์์ฑ ๋ฐฉ์์ ํผ์ฉํ  ์ ์์ต๋๋ค.

- `css` prop๊ณผ์ ํธํ์ฑ์ ํฅ์ ์์ผ์ค๋๋ค.
- ์ฑ๋ฅ์ ๋ํ ๋ณ๋์ ์ธ๊ธ์ ์์ต๋๋ค.

```ts
// string
const BoxByString = styled.div`
  background: palevioletred;
  height: 50px;
  width: 50px;
`;

// object
const BoxByString = styled.div(({ theme }) => ({
  background: "palevioletred",
  height: "50px",
  width: "50px",
  color: theme.colors.red,
}));
```

## Theming

> ๋ผ๋ฒจ๋ง ๋ ์คํ์ผ ๊ฐ์ ํ์ฉํ๊ธฐ ์ํ ์ค์  ์ฐจ์ด๋ฅผ ๊ธฐ์ ํ์ต๋๋ค.

### stitches

`stitches.config.ts` ํ์ผ์ `createStitches` ๋ฅผ ํ์ฉํ์ฌ ์ผ๊ด์ ์ผ๋ก ์์ฑํฉ๋๋ค.

- ๋ณ๋ Provider ํ์ ์์ด ํ๋ง๊ฐ ์ ์ฉ๋ฉ๋๋ค.
- ํ๋ง, ๋ฐ์ํ, ์ ํธ, ํ๋ง๋งต ๋ฑ์ ํ์ฉํ  ์ ์์ต๋๋ค.

```ts
// stitches.config.ts

export const { styled, createTheme, getCssText, ...rest } = createStitches({
  /**
   * theme, media, utils, themeMap ...
   */
});
```

### emotion & styled-components

`theme.ts` ํ์ผ์ ์์ฑํ๊ณ  `<ThemeProvider>` ๋ฅผ ํตํด ์ ๋ฌํฉ๋๋ค.

```ts
// theme.ts

import { Theme } from "@emotion/react";

const theme: Theme = {
  // theme
};

export default theme;
```

```ts
// _app.tsx

export default function App({ Component, pageProps }: AppProps) {
  return (
    <>
      <ThemeProvider theme={theme}>
        <Component {...pageProps} />
      </ThemeProvider>
    </>
  );
}
```

## Variants

> ์ํฉ๋ณ๋ก ์คํ์ผ๋ง์ ๋ณํ๋ฅผ ์ค ์ ์๋ ๋ฐฉ์์ ์ฐจ์ด๋ฅผ ๊ธฐ์ ํ์ต๋๋ค.

### stitches

๋ผ์ด๋ธ๋ฌ๋ฆฌ ๋ด Variant API๋ฅผ ํ์ฉํ์ฌ ๊ตฌํํ  ์ ์์ต๋๋ค.

- `variants` ๋ผ๋ `key` ๋ฅผ ํตํด ์์ฑํ  ์ ์์ต๋๋ค.
- [Multiple variants](https://github.com/p-acid/why-we-use-stitches/tree/main/stitches#multiple-variants%EB%B3%B5%EC%88%98-%EB%B6%84%EA%B8%B0)๊ฐ ๊ฐ๋ฅํฉ๋๋ค.
- [`boolean` ๊ฐ ํธ๋ค๋ง](https://github.com/p-acid/why-we-use-stitches/tree/main/stitches#boolean-variants%EB%B6%88%EB%A6%AC%EC%96%B8-%EB%B6%84%EA%B8%B0) ๋ํ ๊ฐ๋ฅํฉ๋๋ค.
- [Variant ํฉ์ฑ์ ํตํ ์์](https://github.com/p-acid/why-we-use-stitches/tree/main/stitches#compound-variants%EB%B6%84%EA%B8%B0-%EB%82%B4-%EC%8A%A4%ED%83%80%EC%9D%BC-%ED%95%A9%EC%84%B1)๋ ๊ฐ๋ฅํฉ๋๋ค.
- ์ด์ธ [๊ธฐ๋ณธ variant ์ค์ ](https://github.com/p-acid/why-we-use-stitches/tree/main/stitches#default-variants%EA%B8%B0%EB%B3%B8-%EB%B6%84%EA%B8%B0), [๋ฐ์ํ ๋ถ๊ธฐ](https://github.com/p-acid/why-we-use-stitches/tree/main/stitches#responsive-variants%EB%B0%98%EC%9D%91%ED%98%95-%EB%B6%84%EA%B8%B0) ๋ฑ๋ ๊ฐ๋ฅํฉ๋๋ค.

```ts
// ๊ธฐ๋ณธ variant ์ฌ์ฉ๋ฒ

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
```

### emotion & styled-components

`css` ํจ์๋ฅผ ํตํด ๋ถ๊ธฐ๋ณ ์คํ์ผ๋ง ๊ฐ๋ค์ ๊ฐ์ฒด ํํ๋ก ์์ฑํ  ์ ์์ต๋๋ค.

```ts
// css ์คํ์ผ๋ง ๊ฐ์ฒด ์์ฑ ์์

// 1. variant ๋ณ style ๊ฐ์ฒด ์์ฑ
const style = {
  white: css`
    background-color: white;
  `,
  red: css`
    background-color: red;
  `,
  blue: css`
    background-color: blue;
  `,
};

// 2. ํด๋น ์ปดํฌ๋ํธ์ ์คํ์ผ ๋ถ๊ธฐ ์ถ๊ฐ

const Button = styled.button<{ color?: string }>`
  background-color: black; ${/* Default set */}

  ${({ color }) => style[color]}
`;
```

## Responsive

> ํ๋ฉด ์ฌ์ด์ฆ ๋ถ๊ธฐ๋ณ ๋ฐ์ํ ์คํ์ผ๋ง์ ๊ตฌํํ๊ธฐ ์ํ ๋ฐฉ์ ์ฐจ์ด๋ฅผ ๊ธฐ์ ํ์ต๋๋ค.

### stitches

[Theming](https://github.com/p-acid/why-we-use-stitches#theming) ํํธ์์ ์ธ๊ธํ `createStitches` ํจ์๋ฅผ ํตํด ๋ฐ์ํ ๋ถ๊ธฐ๋ฅผ ๊ฒฐ์ ํ  ์ ์๊ณ , ์ด๋ฅผ `@` ์ ๋์ฌ์ ํจ๊ป ํ์ฉํ  ์ ์์ต๋๋ค.

```ts
// ๋ฐ์ํ ๋ถ๊ธฐ ์ค์ 

export const { styled, css } = createStitches({
  media: {
    bp1: "(min-width: 640px)",
    bp2: "(min-width: 768px)",
    bp3: "(min-width: 1024px)",
  },
});
```

```ts
// ํ์ฉ ์์

const Button = styled("button", {
  // base styles

  variants: {
    color: {
      violet: {},
      gray: {},
    },
  },
});

() => (
  <Button
    color={{
      "@initial": "gray", // ๋ฐ์ํ ์ ์ฉ ์  ์ด๊ธฐ ์ํ
      "@bp2": "violet", // bp2 ๋ถ๊ธฐ ์ ์ฉ
    }}
  >
    Button
  </Button>
);
```

### emotion & styled-components

CSS ๋ฏธ๋์ด ์ฟผ๋ฆฌ๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ์๊ณผ ๋์ผํฉ๋๋ค.

> ๊ฒฝ์ฐ์ ๋ฐ๋ผ `react-responsive` ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ๊ฒธ์ฉํ์ฌ ํ์ฉํ  ์ ์์ต๋๋ค.
>
> `facepoint` ๋ผ์ด๋ธ๋ฌ๋ฅผ ํตํด ๋ถ๊ธฐ์ ๋ฐ๋ฅธ ์คํ์ผ ์์ฑ์ ํจ์จ์ ์ผ๋ก ์์ฑํ  ์๋ ์์ต๋๋ค.

```tsx
// ๊ธฐ๋ณธ ์ฌ์ฉ๋ฒ

import { css } from "@emotion/react";

render(
  <p
    css={css`
      font-size: 30px;
      @media (min-width: 420px) {
        font-size: 50px;
      }
    `}
  >
    Some text!
  </p>
);
```

```tsx
// ์ฌ์ฌ์ฉ ๊ฐ๋ฅํ ๋ฏธ๋์ด ์ฟผ๋ฆฌ ํ์ฉ ๋ฐฉ๋ฒ

import { css } from "@emotion/react";

const breakpoints = [576, 768, 992, 1200];

const mq = breakpoints.map((bp) => `@media (min-width: ${bp}px)`);

render(
  <div>
    <div
      css={{
        color: "green",
        [mq[0]]: {
          color: "gray",
        },
        [mq[1]]: {
          color: "hotpink",
        },
      }}
    >
      Some text!
    </div>
  </div>
);
```

## Overriding

> ํน์  ์ปดํฌ๋ํธ ์ค๋ฒ๋ผ์ด๋๋ฅผ ๊ตฌํํ๊ธฐ ์ํ ๋ฐฉ์์ ์ฐจ์ด๋ฅผ ๊ธฐ์ ํ์ต๋๋ค.

### stitches

๊ณต์ ๋ฌธ์ ๊ธฐ์ค `css` prop์ ํตํด ์คํ์ผ ์ค๋ฒ๋ผ์ด๋๊ฐ ๊ฐ๋ฅํ๋ค๊ณ  ํฉ๋๋ค.

- `styled` ํจ์์ ์ฒซ ๋ฒ์งธ ์ธ์๋ก ์ปดํฌ๋ํธ(์ผ๋ฐ, ์คํฐ์น ๋ชจ๋)๋ฅผ ์ง์ ํ์ฌ ์ค๋ฒ๋ผ์ด๋ ํ  ์ ์์ต๋๋ค.
- ๋ํ, `as` prop์ ํตํด ์ปดํฌ๋ํธ์ ๋ ๋๋ง DOM์ ๋ณ๊ฒฝํ  ์๋ ์์ต๋๋ค.

```tsx
// css prop ์ค๋ฒ๋ผ์ด๋

() => (
  <Button
    as="div"
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

```tsx
// styled ์ค๋ฒ๋ผ์ด๋

const Button = styled("button", {
  ...
});

const OverridedButton = styled(Button, {
  backgroundColor: "red",
});
```

### emotion & styled-components

`style` prop์ ํตํ ์ค๋ฒ๋ผ์ด๋์ `styled` ํจ์์์ ํ ์ปดํฌ๋ํธ๋ฅผ ์ง์ ํ์ฌ ์ค๋ฒ๋ผ์ด๋ ํ๋ ๊ฒ ๋ํ ๊ฐ๋ฅํฉ๋๋ค.

- `as` prop์ ํตํ ๋ ๋๋ง DOM ๋ณ๊ฒฝ ๋ํ ๊ฐ๋ฅํฉ๋๋ค.

```tsx
const Button = styled.button`
  background-color: red;
`;

const OverridedButton = styled(Button)`
  background-color: blue;
`;

export default function Example() {
  return (
    <>
      <Button style={{ backgroundColor: "violet" }}>Button</Button>
      <OverridedButton as="div">Button</OverridedButton>
    </>
  );
}
```

## Selector

> ๊ณตํต์ ์ผ๋ก ํ์ฉํ  ์ ์๋ Nested Selector ์์ฑ ๋ฐฉ์์ ์ฐจ์ด๋ฅผ ๊ธฐ์ ํ์ต๋๋ค.
>
> ๊ธฐ๋ณธ์ ์ธ CSS Selector๋ฅผ ์ง์ํฉ๋๋ค.

### stitches

ํ ์ปดํฌ๋ํธ๋ฅผ `string` ๋ณํ์ ํตํด ์ง์ ํ  ์ ์์ต๋๋ค.

```tsx
const Button = styled("button", {
  ...
});

const NestWrapper = styled("div", {
  [`${Button}`]: {
    color: "white",
    background: "Blue",
  },
});

export default function Example() {
  return (
    <NestWrapper>
      <Button color="green">Button</Button>
    </NestWrapper>
  );
}
```

### emotion & styled-components

`string` ์์ฑ ๋ฐฉ์์์ ํํ๋ฆฟ ๋ฆฌํฐ๋ด ๋ด ๋ณ์ ์์ฑ ๋ฐฉ์์ผ๋ก ์ถ๊ฐํ  ์ ์์ต๋๋ค.

- ๊ฐ์ฒด ์์ฑ ๋ฐฉ์์ ๊ฒฝ์ฐ stitches์ ๋์ผํฉ๋๋ค.

```tsx
const Button = styled.button`
  ...
`;

const NestWrapper = styled.div`
  ${Button} {
    color: white;
    background: green;
  }
`;

export default function Example() {
  return (
    <NestWrapper>
      <Button>Button</Button>
    </NestWrapper>
  );
}
```

# References

## Docs

- [Stitches Docs](https://stitches.dev/docs/installation)
- [Emotion Docs](https://emotion.sh/docs/introduction)
- [Styled components Docs](https://styled-components.com/docs)

## Blog

- [SOSOLOG : Design System Decision Record](https://so-so.dev/react/design-system-decision-record/)
- [SOSOLOG : CSS-in-JS, ๋ฌด์์ด ๋ค๋ฅธ๊ฐ์?](https://so-so.dev/web/css-in-js-whats-the-defference/)
  - css-in-js์ ๋ฐ์  ์์ฝ
  - run-time๊ณผ zero-runtime์ ๋์ ๋ฐฉ์ ์ฐจ์ด
  - Atomic CSS ๋ง๋ณด๊ธฐ
  - stitches.js์ near-zero-runtime
- [JBEE.io : Headless UI Library๋?](https://jbee.io/react/headless-concept/)
  - Headless?
  - Why Headless?

## Presentation

- [slideshare : ์ด๋ฒ ์์ ๋์์ธ ์์คํ์ ์ฒ์์ด๋ผ](https://www.slideshare.net/NaverEngineering/ss-248549018)
- [Youtube : feconf - ๋์์ธ ์์คํ, ํํ๋ฅผ ๋์ด์](https://www.youtube.com/watch?v=21eiJc90ggo)
