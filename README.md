# React Job Experience Tabs Component

This is a React application designed to showcase job experience or similar chronological data using an interactive tabbed interface. The application fetches data from an external API and allows users to click through different "tabs" (representing companies or roles) to view the associated details.

**[Live Demo](https://showcasejobtab.netlify.app/)**

## Features

- Fetches job experience data asynchronously from the `course-api.com` endpoint.
- Displays a loading indicator while data is being retrieved.
- Renders a clean, tabbed interface where each tab represents a different job/company.
- Highlights the currently active tab for clear visual feedback.
- Displays detailed information for the selected job, including:
  - Job Title
  - Company Name
  - Employment Dates
  - List of responsibilities/duties
- Dynamically renders the list of job duties using a separate `Duties` component.
- Utilizes `react-icons` for styling elements within the duties list.
- Employs `uuid` for generating unique keys for list items in the `Duties` component.
- Built entirely with functional components and modern React Hooks (`useState`, `useEffect`).
- Demonstrates core React concepts: component composition, state management, props drilling, asynchronous operations, and conditional rendering.

## Tech Stack

- **React:** Core library for building the user interface (`useState`, `useEffect`).
- **Fetch API:** Standard browser API used for asynchronous data fetching.
- **react-icons:** Library for including popular icons in React projects.
- **uuid:** Library for generating unique identifiers.

## Project Structure

/src
├── App.jsx # Main component: fetches data, manages state (loading, jobs, current tab)

├── BtnContainer.jsx # Renders the company/job tab buttons and handles tab switching

├── JobInfo.jsx # Displays the details (title, company, dates, duties) of the selected job

├── Duties.jsx # Renders the formatted list of duties for a specific job

├── index.css # Styles for the components (or your preferred styling solution)

└── index.js # Application entry point


## API Reference

This project fetches data from the `react-tabs-project` endpoint provided by [course-api.com](https://www.course-api.com/):

- **URL:** `https://www.course-api.com/react-tabs-project`
- **Method:** GET
- **Response:** JSON array of job objects, each containing `id`, `order`, `title`, `dates`, `duties`, `company`.

## Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

- Node.js (v14 or later recommended)
- npm (usually comes with Node.js) or yarn

### Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/NoToRacism/ShowcaseJobData
    ```

2.  **Navigate to the project directory:**

    ```bash
    cd <project-directory-name>
    ```

3.  **Install dependencies:**
    This command installs React and other necessary libraries like `react-icons` and `uuid`.
    Using npm:
    ```bash
    npm install
    ```
    or using yarn:
    ```bash
    yarn install
    ```

## Available Scripts

In the project directory, you can run the following standard Create React App scripts:

### `npm start` or `yarn start`

Runs the app in development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser. The page automatically reloads when you make code changes.

### `npm test` or `yarn test`

Launches the test runner in interactive watch mode.

### `npm run build` or `yarn build`

Builds the app for production to the `build` folder. It optimizes the build for the best performance and prepares it for deployment.

## How It Works

1.  **Data Fetching (`App.jsx`):**

    - When the `App` component mounts, a `useEffect` hook calls the `fetchJobs` asynchronous function.
    - `fetchJobs` uses the Fetch API to request data from the specified `url`.
    - While fetching, the `isLoading` state is `true`, causing a loading indicator to be displayed.
    - Once the data is received and parsed as JSON, it's stored in the `jobs` state variable using `setJobs`, and `isLoading` is set to `false`.

2.  **State Management (`App.jsx`):**

    - `isLoading` (boolean): Tracks whether the initial data fetch is complete.
    - `jobs` (array): Stores the array of job objects received from the API.
    - `currentItem` (number): Stores the _index_ of the currently selected job in the `jobs` array. This determines which job's details are displayed. It defaults to `0` (the first job).

3.  **Tab Navigation (`BtnContainer.jsx`):**

    - This component receives the `jobs` array, the current `currentItem` index, and the `setCurrentItem` function from `App` via props.
    - It maps over the `jobs` array to render a `<button>` for each job, displaying the `item.company` name.
    - The button corresponding to the `currentItem` index receives an `active-btn` class for styling.
    - Each button has an `onClick` handler that calls `setCurrentItem(index)`, updating the `currentItem` state in the parent `App` component to the index of the clicked button.

4.  **Displaying Job Details (`JobInfo.jsx`):**

    - This component receives the `jobs` array and the current `currentItem` index from `App`.
    - It accesses the data for the currently selected job using array indexing: `jobs[currentItem]`.
    - It destructures the `company`, `dates`, `duties`, and `title` from the selected job object.
    - It renders the title, company, and dates.
    - It renders the `Duties` component, passing the `duties` array (specific to the selected job) down as a prop.

5.  **Rendering Duties (`Duties.jsx`):**
    - This component receives the `duties` array (a list of strings) as a prop.
    - It maps over the `duties` array. For each `duty` string:
      - It generates a unique `id` using `uuidv4()`.
      - It renders a `div` containing an icon (`FaAngleDoubleRight` from `react-icons`) and the duty text (`<p>{duty}</p>`).
      - The generated `uuid` is used as the `key` prop for the list item `div`.

