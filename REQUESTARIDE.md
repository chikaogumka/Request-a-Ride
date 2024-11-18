## "Reqest a ride" app feature test documentation, checklist and Acceptance criteria.
In this document, the above feature's testing and documentation was describes extensively. A checklist to ensure the execution of this feature's testing has also been included.

## Checklist
1. Functional Requirements
- Verify the feature meets all the requirements specified in the documentation.
- Test expected inputs and outputs for all use cases.
- Ensure edge cases are handled gracefully (e.g., empty inputs, incorrect formats).
- Validate error messages and handling for invalid inputs.
2. Integration Testing
- Confirm the feature integrates seamlessly with other parts of the system.
- Test interactions with APIs, databases, and external systems.
- Validate data flows and dependencies between modules.
3. Regression Testing
- Verify that implementing the feature does not break any existing functionality.
- Test related areas to ensure no unintended side effects.
4. User Interface (UI)
- Check the UI elements related to the feature:
- Correct layout, alignment, and visual design.
- Responsive design across different devices and screen sizes.
- Test accessibility (e.g., keyboard navigation, screen reader compatibility).
- Validate the feature’s interaction workflows and usability.
5. Edge Cases
- Test scenarios that might not be obvious:
- Boundary values (e.g., 0, max length, special characters).
- Unusual user behavior.
- Interrupted actions (e.g., network drop mid-transaction).
6. Localization and Globalization (if applicable)
- Verify the feature works correctly in different languages.
- Check date, time, and number formatting for various locales.
7. Performance (Not in scpoe of test document)
- Measure response time and ensure it meets performance benchmarks.
- Test for scalability (e.g., handling large data volumes or simultaneous users).
- Confirm there is no memory leakage or excessive resource consumption.
8. Security (Not in scope of test document)
- Ensure data validation and sanitization to prevent security issues (e.g., SQL injection, XSS).
- Validate authentication and authorization mechanisms if the feature involves sensitive data.
- Check encryption of sensitive data during storage and transmission.
9. Error Handling and Logs
- Ensure clear and informative error messages are shown for failures.
- Confirm appropriate logging for debugging and auditing purposes.
10. Deployment/Environment
- Confirm the feature works correctly in all targeted environments (e.g., development, staging, production).
- Test under different browser versions or operating systems, if relevant.
11. Documentation and User Guides
- Ensure feature-related documentation is accurate and complete.
- Confirm any in-app guides or tooltips explain the feature effectively.
12. Rollback and Recovery (Not in scope of test document)
- Test rollback scenarios if the feature fails in production.
- Verify that data integrity is maintained after recovery.

## Feature Description
Title: Request a Ride
Scenario:
WHEN I want to "Request a Ride,"
THEN there should be an address picker screen allowing me to set the pickup location and destination(s).

Application Details:
Platform: Bolt App
Installable From: Google Play, App Store
User Registration: Phone number

## Test Setup Prerequisite for "Request a Ride" Feature
Before running any test cases, ensure the following prerequisites are met to create a stable test environment:

- Environment Setup
  - App Installation: Install the latest version of the Bolt app from the Google Play Store or Apple App Store. Ensure the app is updated to the version containing the “Request a Ride” feature. 
  - Network Connection: Ensure a stable internet connection (Wi-Fi or cellular data). Test in an area with sufficient network coverage to simulate real user conditions.

- Device Configuration
  - Supported Devices: Use at least one Android and one iOS device to cover platform-specific behaviors. Ensure the devices meet the app's minimum OS requirements.
  - GPS Settings: Enable GPS/location services on the test device.
  - Grant location permissions to the app during or after installation.
- Test Data
  - User Account: create or use a test account registered via a valid phone number. Ensure the test account is logged in before starting the tests.
  - Address Details: Have a list of test addresses to simulate inputs (valid addresses, invalid inputs, and edge cases such as remote areas). Include commonly used locations for pickup/destination to verify suggestion accuracy.
- Backend and API Readiness
  - API Accessibility: Ensure all required APIs (e.g., location services, maps, and address suggestions) are operational and accessible.
  - Test Environment: Confirm testing in a staging environment, if available, to avoid affecting real users or live data.

- Tools and Utilities
  - Monitoring Tools: Install tools to capture logs (e.g., Logcat for Android, Xcode logs for iOS). Use network monitoring tools like Postman or Charles Proxy to inspect API calls, if needed.
  - Time Simulation: Optionally, use tools to test the feature in different time zones or peak hours.

- Team Readiness
  - Issue Tracking: Ensure an issue tracker (e.g., Jira, Allure) is ready to log any defects identified during testing.
  - Communication: Have communication channels open with the development team in case issues need immediate clarification.

- Cleanup Checklist
  - Environment Reset: Before starting tests, reset the app data or clear caches to simulate a fresh user experience. Ensure no lingering data from previous sessions impacts the test results. By completing these setup steps, the testing process becomes streamlined and ensures reproducible results across multiple test runs.

## Test Cases
### Functional Test cases
1. Address Picker: Pickup Location
Test Case: Validate that the address picker allows users to set a pickup location.
  - Steps:
    - Open the Bolt app.
    - Navigate to the “Request a Ride” feature.
    - Click on the "Set Pickup Location" field.
    - Enter a valid address manually or select from the suggested locations.
  - Expected Outcome:
  The entered or selected address is accurately displayed as the pickup location.
2. Address Picker: Destination
Test Case: Validate that users can set one or more destinations.
  - Steps:
    - Open the Bolt app.
    - Navigate to the "Request a Ride" feature.
    - Click on the "Add Destination" button.
    - Enter multiple valid addresses or select them from the map.
  - Expected Outcome:
  The app should allow setting at least one destination and display them correctly.
3. Geolocation
Test Case: Validate that the app uses the device’s GPS to suggest a default pickup location.
  - Steps:
    - Enable GPS on the device.
    - Open the Bolt app and navigate to the "Request a Ride" screen.
    - Observe the default pickup location suggestion.
  - Expected Outcome:
  The app suggests a pickup location based on current GPS coordinates.
4. Add Multiple Destination Addresses
Test case: Validate the user can add up to 4 addresses and the top of the list is always the pickup location field.
  - Steps:
    - Navigate to the "Request a Ride" screen.
    - Open the address picker screen.
    - Enter the Pickup Location in the top input field (e.g., "123 Test Street").
    - Add a Destination 1 (e.g., "456 Destination Ave").
    - Add a Destination 2 by clicking the plus button "Add Destination" (e.g., "789 Example Blvd").
    - Add a Destination 3 by clicking the plus button "Add Destination" (e.g., "1011 Another Rd").
    - Add a Destination 4 by clicking the plus button "Add Destination" (e.g., "1213 Final Ln").
    - Attempt to add a 5th Destination.
  - Expected Outcomes:
    - Step 2: The entered pickup location ("123 Test Street") is always displayed at the top of the list.
    - Steps 3-6: Each new destination is added below the previous one, maintaining the pickup location as the topmost field
    - Step 7: The app prevents adding a fifth destination and displays a message like: "You can only add up to 4 destinations."
    - The UI dynamically updates to reflect the current state of addresses.
    - The list of addresses contains a maximum of 4 entries: 1 Pickup Location (top) and up to 3 Destinations.

5. Address UI can be rearranged.
Test Case: Validate that the user can rearrange the 4 addresses on the screen, while the Pickup Location placeholder remains fixed at the top.
- Test Steps:
  - Navigate to the "Request a Ride" screen.
  - Add a Pickup Location and up to 3 Destinations (4 total addresses).
  - Open the address list on the "Request a Ride" screen, displaying 1 Pickup Location and 3 Destinations.
  - Attempt to move the Pickup Location to any position other than the top.
  - Rearrange the Destinations by dragging and dropping them to different positions. Example: Move Destination 3 to the second position. Save the updated order (if applicable).
- Expected Outcomes:
  - Step 2: The Pickup Location can be moved but the pickup location place holder remains fixed at the top.
  - Step 3: Destinations can be successfully rearranged, and the new order is reflected in the list.
  - Step 4: The rearranged order is preserved after saving or navigating away from the screen.
Notes:
Test both drag-and-drop gestures and any alternative reordering mechanisms (e.g., arrows, dropdowns).
Verify that the displayed order matches the internal logic used for routing and navigation.
Ensure no unexpected crashes or UI glitches occur during or after the reordering process.

6. User Can Delete Addresses
Test case: Validate the user can delete pickup or destination addresses.
-Test Steps:
  - On the address picker screen, locate the list of added addresses from test case 5 (pickup and destinations).
  - Attempt to delete Destination 2 by using the delete option (e.g., a trash icon, swipe, or contextual menu).
  - Attempt to delete Destination 1 and confirm the action if prompted.
  - Attempt to delete the Pickup Location and confirm the action if prompted.
  - After each deletion, observe the list and ensure the remaining addresses are reordered correctly.
- Expected Outcomes:
  - Step 2: Destination 2 is successfully removed, and the remaining destinations shift up to fill the gap.
  - Step 3: Destination 1 is successfully removed, and the remaining destinations reorder dynamically.
Notes:
Test for multiple deletion methods, such as swipe-to-delete and selecting the delete option in the contextual menu.
Ensure confirmation dialogs, if any, are user-friendly and prevent accidental deletions.
Verify the functionality on both Android and iOS platform

### Integration Testing
1. Map Integration
Test Case: Verify the map functionality in the address picker.
- Steps:
  - Open the address picker screen.
  - Use the map to select a location by dragging and dropping the pin.
Expected Outcome:
  - The map updates the pickup/destination address when the pin is moved.
2. Address Suggestions
Test Case: Validate integration with the location service API (e.g., Google Places API).
- Steps:
  - Start typing an address in the pickup or destination field.
  - Check for suggestions.
- Expected Outcome:
  - Address suggestions appear dynamically as the user types.

### User Interface Testing (UI)
1. Layout Validation
Test Case: Ensure that the address picker screen follows the app’s design guidelines.
- Steps:
  - Open the address picker screen.
  - Verify the alignment, fonts, colors, and interactive elements.
Expected Outcome:
- The screen matches the design specifications.
2. Usability
Test Case: Test that users can switch between pickup and destination input seamlessly.
- Steps:
  - Open the address picker screen.
  - Enter a pickup location, then switch to destination(s).
- Expected Outcome:
  - Smooth navigation without any freezing or delays.

### Performance
1. Response Time
Test Case: Measure the time taken to fetch address suggestions.
- Steps:
  - Enter a partial address in the input field.
  - Measure the time until suggestions appear.
- Expected Outcome:
  - Address suggestions should load in less than 2 seconds.
2. GPS Accuracy
Test Case: Test the accuracy of the GPS-based location suggestion.
- Steps:
  - Move to a known location.
  - Open the app and observe the suggested pickup location.
Expected Outcome:
  - The suggested pickup location is within a 10-meter radius.

### Error Handling
1. Invalid Address
Test Case: Validate behavior when the user enters an invalid or incomplete address.
- Steps:
  - Enter an address like "xyz" in the input field.
  - Attempt to confirm the location.
Expected Outcome:
  - An error message like "Invalid address. Please select a valid location" appears.
2. GPS Disabled
Test Case: Test behavior when GPS is disabled.
- Steps:
  - Turn off GPS.
  - Open the "Request a Ride" screen.
- Expected Outcome:
  - A prompt asks the user to enable GPS, or manual address input is required.

### Edge Cases
1. Remote Areas
Test Case: Test functionality in a remote area with weak or no network connectivity.
- Steps:
  - Move to a location with limited connectivity or use a simulated low internet connection.
  - Try setting the pickup and destination.
- Expected Outcome:
  - The app handles the situation gracefully, with offline prompts if applicable.
6.2 Multiple Destinations
Test Case: Test behavior with more than the allowed number of destinations.
Steps:
  - Add multiple destinations until reaching the limit.
  - Try adding one more.
- Expected Outcome:
  - The app prevents adding more destinations and shows a relevant message.

### Localization
Test Case: Validate address formatting for different locales (e.g., U.S. vs. Europe).
- Steps:
  - Change the app’s locale to a different region.
  - Test address inputs and suggestions.
- Expected Outcome:
  - Addresses appear in the correct format for the selected locale.

### Test cases for Regression and Smoke testing
The test cases written for these use cases are core feature functionality. Every regression test is supposed to validate that all the previous feature functionality still works as expected hence why these where chosen. Also, the test cases under this section can be checked really quickly to validate a hot fix, business critical and core functionality if all the preconditions for the test has already been setup, hence why they are excellent for smoke testing.
#### For Smoke Testing
These test cases verify the basic functionality and serve as a quick check for system readiness:
- Validate the user can add up to 4 addresses, and the top is always the pickup location.
Ensures critical address addition functionality works.
- Validate the user can set a pickup location.
Ensures users can specify a starting point, a core feature.
- Validate the user can set a destination.
Ensures users can specify where they want to go, essential to ride requests.
- Verify the "Request a Ride" screen opens correctly.
Ensures the feature loads without crashing.

#### For Regression Testing
These test cases cover a broader range of scenarios and ensure no unintended consequences of updates:
- Validate the user can add up to 4 addresses, and the top is always the pickup location.
Checks address handling logic, which may be impacted by changes.
- Validate the 4 addresses can be rearranged on the screen.
Ensures drag-and-drop or reordering functionality is unaffected by updates.
- Validate the user can delete addresses.
Ensures deletion functionality works as intended after changes.
- Validate the user can set a pickup location.
Ensures a core feature remains functional after updates.
- Validate the user can set a destination.
Covers a primary functionality critical to ride requests.
- Edge Cases and Error Handling:
Include tests for invalid input (e.g., entering invalid addresses) to ensure robust handling after system updates.

### Documentation and Notes
2. Known Limitations
Address suggestions may depend on third-party APIs, which could have outages.
3. Dependencies
GPS service.
External APIs for address lookup.
These test cases cover functional, UI, integration, and edge aspects, ensuring thorough validation of the feature.
