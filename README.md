


## PawConnect(Pet Adoption and Care)

Description-Discover your perfect pet companion with ease! This app offers a rich, tailored browsing experience with filters for pet type, age, and size, along with personalized recommendations based on user preferences. Detailed pet profiles provide insight into each pet's personality, health, and care needs, with interactive maps to locate nearby adoption centers. Users can set reminders for care activities, mark pets of interest, and receive real-time adoption updates.  An engaging community forum, the app is designed to simplify pet adoption while offering valuable resources for pet care and companionship.

## Features by Pages

### 1. **Home Page**
   - A visually appealing landing page introducing users to the platform's mission and key functionalities.
   - Navigation to major sections: adoption, nearby services, tips, and more.

### 2. **Pet Adoption Page**
   - Search and filter pets by attributes like type, breed, age, size, and health.
   - Detailed profiles of pets available for adoption, with options to express interest.

### 3. **NGO Management Page**
   - Tools for NGOs to add themselves on the webpage
   - Approve and Pending status

### 4. **Nearby NGO and Pet Care Services**
   - Real-time integration with Google Maps API to locate NGOs, veterinary clinics, and pet care providers.
   - Displays location-based services for user convenience.

### 5. **Pet Food Product Page**
   - Explore a curated selection of pet food products categorized by pet type and dietary requirements.
   - Filter options for selecting the best food based on health needs.

### 6. **Tips Page**
   - A library of expert articles covering topics like grooming, training, and emergency care.
   - Seasonal and situation-specific pet care advice for owners.

### 7. **Diet Generator Page**
   - Generate customized diet plans based on your pet's type, breed, weight, and health conditions.
   - Provides easy-to-follow nutrition guidelines tailored to each pet.

## Technology Stack
- **Frontend**: React, TypeScript, CSS for a responsive and interactive user interface.
- **State Management**: Redux for managing global state and enabling efficient data flow across components.
- **Backend**: Node.js, Express.js for API development and business logic.
- **Database**: MongoDB for managing dynamic data, such as pet profiles and user records.
- **APIs**: Google Maps API for geolocation services.
- **Real-Time Communication**: Fugu for implementing chat and communication between users and shelters.
- **Hosting**: Deployed on a scalable cloud-based platform.

## Project Structure
The project is modularly structured with clear separation of concerns:

- **/frontend**: React components, Redux stores, and stylesheets for the user interface.
- **/backend**: Node.js API logic, services, and database models.
- **/assets**: Media files such as images, icons, and logos.
- **/config**: Environment variable setup and server configurations.
- **/scripts**: Utility scripts for automation or data setup.

## Dependencies
The following dependencies are required to run the project:

### Backend
- `express`: For building the RESTful API.
- `mongoose`: For connecting and managing the MongoDB database.
- `dotenv`: For managing environment variables.
- `cors`: To enable Cross-Origin Resource Sharing.
- `body-parser`: Middleware for parsing JSON and URL-encoded payloads.

### Frontend
- `react`: For building the user interface.
- `react-dom`: Rendering React components.
- `react-router-dom`: For handling client-side routing.
- `axios`: For making HTTP requests.
- `redux`: For state management.
- `react-redux`: To connect React components with Redux stores.
- `typescript`: For static type checking in React components.

### Communication
- `fugu`: For real-time chat and communication between users.

### Development Tools
- `nodemon`: For live-reloading the backend during development.
- `webpack`: For bundling frontend assets.
- `babel`: For transpiling modern JavaScript code.

## How to Run the Project

### 1. Clone the Repository
```bash
git clone <repository-url>
cd final-project-webarchitects-main
```

### 2. Install Dependencies
Install the required dependencies for both backend and frontend:
```bash
# Navigate to the backend folder and install dependencies
cd backend
npm install

# Navigate to the frontend folder and install dependencies
cd ../frontend
npm install
```

### 3. Setup Environment Variables
Create a `.env` file in the backend folder with the following variables:
```
MONGO_CONNECTION=mongodb+srv://<username>:<password>@cluster.mongodb.net/pawconnect
PORT=3002
GOOGLE_MAPS_API_KEY=<your-google-maps-api-key>
FUGU_API_KEY=<your-fugu-api-key>
```

### 4. Start the Backend Server
```bash
cd backend
npm start
```

### 5. Start the Frontend Development Server
```bash
cd ../frontend
npm start
```

### 6. Open the Application
Visit `http://localhost:3002` in your web browser to access the platform.

## Future Enhancements
- **Mobile Application**: Expand accessibility with native Android and iOS apps.
- **AI-Powered Pet Matching**: Suggest pets based on user preferences and history.
- **Advanced Analytics for NGOs**: Provide insights into adoption trends and operational efficiency.
- **Community Forum**: Create a space for pet owners to share experiences and tips.

## Contributors
- **Team Name**: Web Architects  
- Dedicated to creating impactful digital solutions for pet welfare.

## License
This project is licensed under the MIT License.  
Feel free to contribute, fork, or modify the repository for personal and educational use.

---
We hope PawConnect transforms how you connect with pets and supports our shared mission of animal welfare!


Object Model:

# Domain Model for PawConnect

```mermaid
---
title: PawConnect Model
---

classDiagram
    %% User to NGO and Donations
    User "1" --o "*" OrganizationPost : views
    User "1" --o "*" NGO : volunteers at
    User "1" --o "*" Donation : donates to
    User "1" --o "*" Pet : shows interest in
    
    %% NGO and Pets/Posts
    NGO "1" --o "*" Donation : accepts
    NGO "1" --o "*" OrganizationPost : creates

    %% PetCare Context and Health Details
    Pet "1" --o "1" PetCare : has
    PetCare "1" --o "1" Veterinarian : redirects
    PetCare "1" --o "1" PetSalon : redirects
    PetCare "1" --o "1" PetTherapy : redirects
    PetCare "1" --o "1" DietPlan : redirects
    PetCare "1" --o "*" FoodProduct : redirects

    %% Relationships to NGO and Pets
    NGO "1" --o "*" Pet : owns
    
    %% Diet Plan and Food Products
    DietPlan "*" --o "*" FoodProduct : contains

    %%Location Usage (Value Object)
    Veterinarian "1" --o "*" Location : uses
    PetSalon "1" --o "*" Location : uses
    PetTherapy "1" --o "*" Location : uses
    NGO "1" --o "*" Location : uses
    
    %% Classes
    class User {
        +userId: UUID
        +name: String
        +email: String
        +password: String
        +location: Location
    }

    class Pet {
        +petId: UUID
        +type: String
        +breed: String
        +age: Int
        +size: String
        +disabilityStatus: Boolean
        +healthConcerns: List<HealthConcern>
        +profileImage: String
    }

    class NGO {
        +ngoId: UUID
        +name: String
        +location: Location
        +contactInfo: String
        +description: String
    }

    class OrganizationPost {
        +postId: UUID
        +title: String
        +content: String
        +date: Date
        +ngoId: UUID
    }

    class PetCare {
        +type: String
        +frequency: String
    }

    class Veterinarian {
        +vetId: UUID
        +name: String
        +specialization: String
        +contactInfo: String
        +location: Location
    }

    class PetSalon {
        +salonId: UUID
        +name: String
        +services: List<String>
        +location: Location
        +contactInfo: String
    }

    class PetTherapy {
        +therapyId: UUID
        +name: String
        +type: String
        +location: Location
        +contactInfo: String
    }

    class DietPlan {
        +dietId: UUID
        +foodType: String
        +feedingSchedule: String
        +allergies: List<String>
    }

    class Donation {
        +donationId: UUID
        +amount: Double
        +userId: UUID
        +date: Date
        +purpose: String
    }

    class FoodProduct {
        +productId: UUID
        +name: String
        +brand: String
        +description: String
        +nutritionDetails: String
    }

    %% Location as a Value Object
    class Location {
        +latitude: Double
        +longitude: Double
        +address: String
    }
