**GitHub Repository:**

[Github Repo](https://github.com/Kelvinblaze/employee-data-table)

Instructions to Run Locally:

Clone the repository: git clone https://github.com/Kelvinblaze/employee-data-table.git

Navigate to the project directory: cd your-project-directory

Install dependencies: npm install

Create a .env file in the project root and add the Directus Bearer token:

makefile

Copy code

VITE_DIRECTUS_TOKEN=[TOKEN]

Run the application: npm run dev

Open your browser and go to generated port from the terminal to view the application.

Approach:

**Project Setup:**

- Created a new Vue.js project using Vite: npm create vite@latest my-vue-app.

- Set up the project structure and installed necessary dependencies.

**Styling:**

- Integrated Tailwind CSS for styling as per the provided requirements.

- Used the Figma mockup image as a reference to ensure the application is responsive.

**Data Fetching:**

- Utilized Vue Query and Directus SDK to fetch data from the provided Directus API endpoint.

- Implemented error handling and loading state during data fetching.

**Displaying Data:**

- Designed components to display employee information based on the Figma mockup image.

- Ensured that the layout and styling match the provided design.

**Assumptions:**

- Assumed that the provided Directus endpoint will always return data in the expected format.

- Assumed a constant structure for the employee data and did not account for potential variations.

**Possible Improvements:**

- Implement pagination for the employee list in case the dataset grows.

- Enhance error handling to provide more meaningful error messages to the user.

- Add unit tests to ensure the reliability of the application.

- Optimize the application for better performance, especially when dealing with a large dataset.

Time Spent: [2-4 hours]

**Notes:**

*Feel free to reach out if you have any questions or need further clarification. Thank you for the opportunity!*