# npm stats learning project

Welcome! It's time for your first project exercise at Vaadin.

The goal of this assignment is to become familiar with some of the projects that we build, and tools
that we use.

Even though we believe you are experienced developer, we suggest you to spend at least a few days on
the training project before you switch to the real tasks. Consider this as a chance to learn and to
build something useful.

If you like the idea of doing such small hobby projects that help you to switch context and at the
same time could benefit our team and our community, excellent! That's exactly why we have
Community Focus time at Vaadin.

## 1. General

The project is a single page application to show npm downloads statistics for Vaadin components.
You will need to load the data from JSON endpoints and visualize it using web components from the
Vaadin Design System.

Some recommendations:

1. Please organize the workflow as if you are assigned to build the actual real world application.
2. When you start a project, create a new repository and invite your technical mentor to join.
3. Please split your code into small PRs and assign your technical mentor as a reviewer.
4. If you feel that our [documentation](https://vaadin.com/docs/latest/) is confusing or incomplete, please let the team know!

## 2. Project setup

1. Init an application project using [Open Web Components](https://open-wc.org/docs/development/generator/) generator
2. Answer the questions from the CLI prompt to scaffold the app
3. Choose "Yes" for TypeScript, linting, testing, and bundling

## 3. Technical requirements

Please use the following parts of Vaadin to implement the app:

- [Vaadin Design System](https://vaadin.com/docs/latest/ds/overview) as a UI component library
- [Vaadin Router](https://vaadin.com/docs/latest/fusion/routing/router) for navigating between pages

You can install the latest versions of web components and router by using:

```sh
npm install @vaadin/vaadin@next
```

Additionally, you will need to use a set of tools in your app:

- [Web Dev Server](https://modern-web.dev/docs/dev-server/overview/) for local development
- [Web Test Runner](https://modern-web.dev/docs/test-runner/overview/) for writing unit tests
- [ESLint and Prettier](https://open-wc.org/guides/tools/linting-and-formatting/) for linting and formatting
- [Rollup](https://open-wc.org/docs/building/rollup/) to bundle for production

## 4. First component

Please start by creating a `<date-range-selector>` **reusable web component** shared by different parts of the UI.

There should be a form with 3 fields:

- select a pre-defined date range (last 2 weeks, last 4 weeks) or a custom range
- select a "from" date as a custom range start
- select a "to" date as a custom range end

Note:

- "From" and "To" fields should be disabled if a pre-defined range is selected.
- It shouldn't be possible to select invalid range (e.g. start date is after end).
- Regardless of chosen day of week, the range should start on that week's Monday.

## 5. UI structure

Below you will find a general description and screenshots of the application UI mockups.

1. Please use Vaadin Design System and follow its guidelines to pick the components that you need.
2. Use the HTML files in the `mockup` folder useful as a hint on which components to choose.
3. You **don't have to implement the whole application**. Please focus on trying different components.

### Layout

All the pages (views) share the same layout, which has following sections:

- Navbar with a title and button to toggle sidebar
- Sidebar with a navigation to switch between views:
  - Overview - should be a link to the default view (marked as active)
  - Components - should be a collapsible section with items for individual components views.
- Content - should contain a view content depending on the navigation.

### Overview page

<details>
  <summary>Screenshot</summary>
  <img src="screenshots/overview.png" style="width: 1036px;">
</details>

The overview page should display the following content:

#### Date range selector

Please use the `<date-range-selector>` component that you created in this view.

#### Component selector

There should be a field with autocomplete and a list of suggestions.

- Dropdown items should represent the individual Vaadin components.
- List of components should be the same as in the Sidebar navigation.
- Selecting a component imports the data for it by fetching a JSON API.
- After the data is loaded, the chart and data table are updated (see below).
- After the data for component is updated, the field should be cleared.

#### Downloads chart

There should be a **line chart** with a series representing individual components.

- Data on the chart should represent downloads over time per component.
- When a new component is added, the chart should be redrawn to show it.

#### Data table

There should be a table with several columns to show the downloads.

- First column should contain the checkboxes to toggle row selection.
- When a new row is added to the table, it should be selected by default.
- Selecting a row makes the corresponding series appear in the chart.
- Unselecting a row removes a corresponding series from the chart.
- Component names in the second column should be links to npm packages.
- Downloads columns should be grouped together as shown in the mockup.

### Component page

<details>
  <summary>Screenshot</summary>
  <img src="screenshots/component.png" style="width: 1031px;">
</details>

Every component's page should display the following content:

#### Title

The title should contain a component and match the active link in the Sidebar.

#### Date range selector

Please use the `<date-range-selector>` component that you created in this view.

When a new date range is selected, chart and the data table is updated.

#### Threshold field

There should be a field to set a threshold (minimum count of downloads).

- The field should only accept correct values (numbers > 0)
- Typing a value updates the chart and data table (see below).
- There should be a default value set on the field, e.g. 100.

#### Downloads chart

There should be a **stacking area chart** with a series representing individual versions.

- Data on the chart should represent downloads over time per component version.
- The chart should only include npm versions with downloads above threshold.

#### Data table

There should be a table with several columns to show the downloads per version.

- First column should contain the npm versions of the component.
- Other columns should contain downloads per week (e.g. 1/03, 8/03).
- The table should only show versions with downloads above threshold.
- Typing a new threshold should update the table (add / remove rows).
- Choosing a version range should update the table (add / remove columns).
- It should be possible to sort table by each column, including version.

## 5. Implementation

### JSON API

You will need the following API to implement the application:

1. List of components can be obtained from the Platform repository:

https://raw.githubusercontent.com/vaadin/platform/master/versions.json

2. Individual components stats can be obtained from the following files:

https://github.com/web-padawan/npm-downloads/tree/master/docs

Example: https://web-padawan.github.io/npm-downloads/vaadin-accordion.json

### Routes

Please use Vaadin Router and create routes based on the app structure.
Every route should have a corresponding link from the sidebar.

### State

You don't have to use any state management, it's enough to keep data in properties.

### Tests

Please write unit tests for the `<date-range-selector>` component.
