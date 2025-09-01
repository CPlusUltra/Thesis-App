# Thesis-App
a repository to collaborate on thesis app
![rider app design](https://github.com/CPlusUltra/Thesis-App/blob/main/rider.jpg?raw=true)
![passenger app design](https://github.com/CPlusUltra/Thesis-App/blob/main/passenger.jpg?raw=true)

# Jeepney Finder App Documentation

This document outlines the core specifications, features, and components of the Jeepney Finder app, intended for developers who will continue this project.

## 1. Core Functionality & Purpose

The app solves the inconvenience of waiting for jeepneys by providing real-time tracking and alerts.

### **Features**

* **Alert System:** Alerts passengers when a tracked jeepney is within a fixed 5-minute ETA. Users can dismiss the notification. A known bug is the re-triggering of the alert if the ETA fluctuates.
* **Map with Markers:** Displays the real-time location of both passengers and "on-route" jeepneys. Markers only show location; no additional information like passenger count or capacity is displayed.
* **ETA/Distance Calculation:** The ETA is a simple calculation using the `LocationSensor.Distance` block in MIT App Inventor, based on GPS coordinates. This method does not account for traffic or route deviations, which are known bugs.
* **Jeepney Selection:** Passengers can choose a specific jeepney to track. If no selection is made, the app defaults to tracking the closest jeepney.

---

## 2. User & Data

### **User Journeys**

* **Passenger:** Logs in, views the map, selects a jeepney (or defaults to the closest), and receives a 5-minute ETA alert. The trip has no "end state" and the driver is not notified of the passenger boarding.
* **Driver:** Logs in, toggles an "on-route" button to broadcast their location. The driver's app is an MVP for broadcasting only; they cannot see passengers or ride requests.

### **Data & Storage**

* **Data Storage:** Uses Firebase Realtime Database to store and update real-time coordinates. Data is updated only when the device's GPS location changes.
* **Data Persistence:**
    * **Email/Password Users:** Data is persistent if the user doesn't log out.
    * **Anonymous Users:** All data is lost when the app is closed. This is for new users to test the app without commitment.
* **Local-Only Data:** "Trip" or "request" data is not stored in the database. The connection between a passenger and a selected jeepney is handled locally and is lost upon app closure.
* **Offline State:** Drivers can go offline by toggling the "on-route" button. Both user types go offline when the app is closed.

---

## 3. Technology & Architecture

### **Frontend: MIT App Inventor**

The app is built using MIT App Inventor.

* **UI Components:** Includes `Map Component`, `Location Sensor`, and standard UI elements like buttons, text boxes, and labels.
* **Built-in Functions:** Uses the `Notifier` for alerts and the `Clock` for timing.
* **Extensions:** Relies on the `FirebaseDB Extension` for database interaction and the `SignInWithEmailandPassword Extension` for authentication.

### **Backend: Firebase**

The backend is managed by Google's Firebase.

* **Firebase Realtime Database:** The primary NoSQL database for real-time location and status data.
* **Firebase Authentication:** Manages all user accounts, including persistent email/password and anonymous accounts.

### **External Services & Physical Hardware**

* **OpenRouteService API:** Integrated for navigation and displaying accurate road networks.
* **Android Device:** The platform for the compiled `.apk` file.
* **BLE Beacons:** A planned component for future Assisted GPS tracking.

---

## 4. GitHub Workflow for MIT App Inventor

MIT App Inventor doesn't have native Git integration, so GitHub is used for manual version control.

### **Workflow**

1.  **Export Project:** Export your project as an `.aia` file from the "Projects" menu in MIT App Inventor.
2.  **Create Repository:** Create a new repository on GitHub to store your `.aia` files.
3.  **Upload File:** Upload the `.aia` file to your GitHub repository with a clear commit message.
4.  **Import Project:** To work on a project, import the `.aia` file from your computer back into MIT App Inventor. Note that this creates a new project copy.
