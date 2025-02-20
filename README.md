
# 🚗 Car Trading API

This is the backend for a **Car Trading Platform**, where users can list cars for sale, leave reviews, and manage their listings. The system supports authentication, CRUD operations, image uploads, and reviews.

---

## 📌 Features

✅ **User Authentication:** Register/Login with JWT authentication.  
✅ **Admin Role:** Only admins can add or delete car listings.  
✅ **CRUD Operations:** Users can view cars, admins can create, update, and delete listings.  
✅ **Reviews:** Users can leave reviews on car listings.  
✅ **Image Uploads:** Supports file uploads for car images.  
✅ **MongoDB Database:** Stores users, listings, and reviews.

---

## ⚙️ Tech Stack

- **Node.js + Express.js** - Backend framework
- **MongoDB + Mongoose** - NoSQL Database
- **JWT Authentication** - Secure user authentication
- **Multer** - For image uploads
- **Bcrypt** - For password hashing
- **Cors + Dotenv** - Security and environment management

---

## 📂 Project Structure

```
📦 car-trading-api  
 ┣ 📂 models         # Database models  
 ┃ ┣ 📜 User.js  
 ┃ ┣ 📜 Car.js  
 ┃ ┗ 📜 Review.js  
 ┣ 📂 routes         # API endpoints  
 ┃ ┣ 📜 auth.js      # Authentication routes  
 ┃ ┣ 📜 cars.js      # Car listing routes  
 ┃ ┗ 📜 reviews.js   # Review routes  
 ┣ 📂 middlewares    # Middleware for authentication  
 ┃ ┗ 📜 auth.js  
 ┣ 📂 uploads        # Stored car images  
 ┣ 📜 server.js      # Main server file  
 ┣ 📜 .env           # Environment variables  
 ┣ 📜 package.json   # Dependencies  
 ┗ 📜 README.md      # Documentation  
```

---

## 🚀 Installation & Setup

### 1️⃣ Clone Repository
```bash
git clone https://github.com/your-repo/car-trading-api.git
cd car-trading-api
```

### 2️⃣ Install Dependencies
```bash
npm install
```

### 3️⃣ Configure Environment Variables
Create a `.env` file in the root directory and add:
```
PORT=5001  
MONGO_URI=your_mongodb_connection_string  
SECRET_KEY=your_jwt_secret_key  
```

### 4️⃣ Start the Server
```bash
npm start
```
or
```bash
nodemon server.js  # For auto-restart during development
```

---

## 📌 API Endpoints

### 🔑 **Authentication**
| Method | Endpoint         | Description |
|--------|----------------|-------------|
| POST   | `/api/register` | Register a new user |
| POST   | `/api/login`    | Login and get JWT token |

### 🚗 **Car Listings**
| Method | Endpoint           | Description |
|--------|------------------|-------------|
| GET    | `/api/cars`      | Get all cars |
| POST   | `/api/cars`      | Add a new car *(Admin only)* |
| PUT    | `/api/cars/:id`  | Update a car *(Admin only)* |
| DELETE | `/api/cars/:id`  | Delete a car *(Admin only)* |

### 📝 **Reviews**
| Method | Endpoint             | Description |
|--------|----------------------|-------------|
| GET    | `/api/reviews/:carId` | Get reviews for a car |
| POST   | `/api/reviews`        | Add a review *(Authenticated users only)* |

---

## 📂 Database Schema

### **User Model (User.js)**
```js
const mongoose = require("mongoose");

const UserSchema = new mongoose.Schema({
    username: { type: String, required: true, unique: true },
    password: { type: String, required: true },
    role: { type: String, enum: ["user", "admin"], default: "user" }
});

module.exports = mongoose.model("User", UserSchema);
```

### **Car Model (Car.js)**
```js
const mongoose = require("mongoose");

const CarSchema = new mongoose.Schema({
    title: { type: String, required: true },
    price: { type: Number, required: true },
    specs: {
        mileage: { type: Number, required: true },
        engine_volume: { type: Number, required: true },
        transmission: { type: String, required: true },
        drive_type: { type: String, required: true },
        color: { type: String, required: true }
    },
    imageUrl: { type: String, default: "" },
    userId: { type: mongoose.Schema.Types.ObjectId, ref: "User" },  // Linking to the user who posted it
    reviews: [{ type: mongoose.Schema.Types.ObjectId, ref: "Review" }] // Linking reviews
});

module.exports = mongoose.model("Car", CarSchema);
```

### **Review Model (Review.js)**
```js
const mongoose = require("mongoose");

const ReviewSchema = new mongoose.Schema({
    carId: { type: mongoose.Schema.Types.ObjectId, ref: "Car", required: true },
    userId: { type: mongoose.Schema.Types.ObjectId, ref: "User", required: true },
    username: { type: String, required: true },
    rating: { type: Number, required: true, min: 1, max: 5 },
    comment: { type: String, required: true }
}, { timestamps: true });

module.exports = mongoose.model("Review", ReviewSchema);
```

---

## 🔐 Authentication & Roles

- Users must log in to leave reviews.
- Only **admins** can create, edit, or delete car listings.
- JWT tokens are used for authentication in requests.

---

## 🖼️ Image Uploads

- Cars can have images uploaded using **Multer**.
- Images are stored in the `/uploads` folder.

---

## 📌 Future Improvements

✅ Add search & filtering for listings.  
✅ Implement pagination for large datasets.  
✅ Allow users to edit/delete their own reviews.  
✅ Integrate external APIs for automatic car data retrieval.

---

## 📩 Contact

If you have any questions, feel free to contact me at **231560@astanait.edu.kz, 230020@astanait.edu.kz**.

---

