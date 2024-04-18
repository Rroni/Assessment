### Custom Game Table Technical Assessment

**Objective:** Develop a custom game table web application that matches the design provided in the screenshot. Your application will retrieve game data from an external API and display it in a table with specified columns.

**Project Overview:**
- You will use the attached screenshot as your design reference. The game table includes columns for the game's name, producer, minimum bet, maximum bet, qualification ID, and game version.
- Your task is to replicate this design and functionality in a web application, ensuring the final product closely matches the visual structure and content layout.

**Functional Requirements:**
- **Data Fetching:** Retrieve game data from the provided API endpoint: [Game List API](https://gamelistmiddleware.azurewebsites.net/gamelist).
- **Table Creation:** Dynamically create a table that displays the following columns based on the API response:
  - Game (name of the game)
  - Producer (company that produced the game)
  - Min Bet (minimum bet amount)
  - Max Bet (maximum bet amount)
  - Qualification ID (identification code for the game's qualification)
  - Game Version (version number of the game)
- **Responsive Layout:** The table should be clearly readable on both desktop and mobile devices, resembling the structure in the screenshot.

**Technical Requirements:**
- **Error Handling:** Develop error handling for failed API requests or unexpected data issues.
- **Loading Indicator:** Include a loading indicator that displays while the game data is being fetched.
- **Style Matching:** Match the styling of the table as closely as possible to the screenshot, including fonts, colors, and spacing.

**Technologies to Use:**
- **HTML/CSS:** Utilize HTML and CSS to replicate the table design and responsiveness.
- **JavaScript:** Employ JavaScript for fetching the API data and manipulating the DOM to populate the table.

**Assessment Criteria:**
- **Accuracy:** How closely your implemented table matches the design in the screenshot.
- **Code Quality:** The readability, organization, and efficiency of your code.
- **Functionality:** The correct and bug-free functionality of the data fetching and table population.
- **Design Adaptability:** The responsiveness and visual integrity of the table across various screen sizes.

**Additional Considerations:**
- Think about the user experience of interacting with your table. How could you enhance the usability of your table with additional features or design elements?
- If you were to implement a feature to filter the games by the producer, describe how you would adjust the UI and what logic you would add to your code to support this functionality.

**Deliverables:**
- Push your complete source code to a GitHub repository, ensuring the README includes setup and run instructions. A live demo is not mandatory but would be viewed favorably.

**Time Management Suggestions:**
- Use the first phase of your time to understand the API structure and plan your development approach.
- Prioritize establishing the table structure and ensuring data is correctly retrieved and displayed.
- Focus on replicating the design details in the latter half of your allotted time, followed by thorough testing on different devices to ensure responsiveness.
