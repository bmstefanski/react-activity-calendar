# RSC Activity Calendar

[![CI](https://github.com/bmstefanski/rsc-activity-calendar/actions/workflows/test.yml/badge.svg)](https://github.com/bmstefanski/rsc-activity-calendar/actions/workflows/test.yml)

A flexible RSC to display activity data in a calendar (heatmap).

![Screenshot](screenshot.png?v5)

**[Documentation (Storybook)](https://grubersjoe.github.io/react-activity-calendar)**

## Installation

```shell

npm install rsc-activity-calendar
```

## Data source

The library doesn't include data fetching to avoid forcing you to use a specific data source or HTTP
library. 

Here's a snippet you might find helpful:

```ts
const getCachedContributions = unstable_cache(
  async () => {
    const response = await fetch('https://github-contributions-api.jogruber.de/v4/<username>');
    const data = (await response.json()) as Response;
    const total = data.total[new Date().getFullYear()];

    return { contributions: data.contributions, total };
  },
  ['github-contributions'],
  { revalidate: 60 * 60 * 24 },
);
```

If you don't want to use `github-contributions-api.jogruber.de` or find it not working, you can self-host it here: [grubersjoe/github-contributions-api](https://github.com/grubersjoe/github-contributions-api)
 
## Features

- any number of activity levels 📈
- color themes 🌈
- localization 🌍

The component expects activity data in the following structure. Each activity level must be in the
interval from 0 to `maxLevel`, which is 4 per default (see
[documentation](https://grubersjoe.github.io/react-activity-calendar/?path=/story/react-activity-calendar--activity-levels)).

It is up to you how to generate and classify your data.

```json
[
  {
    "date": "2023-06-14",
    "count": 2,
    "level": 1
  },
  {
    "date": "2023-06-22",
    "count": 16,
    "level": 3
  }
]
```

## Development

### Start the Storybook

```shell
npm run dev
```

### Update the documentation

```shell
npm run build:storybook
```

## Related projects

- [grubersjoe/react-github-calendar](https://github.com/grubersjoe/react-github-calendar)
- [grubersjoe/github-contributions-api](https://github.com/grubersjoe/github-contributions-api)
