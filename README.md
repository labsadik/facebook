
# 🎨 Pinterest Clone

A fully functional Pinterest-style platform with image/video sharing, user auth, and masonry grid layout.

---

## ✨ **FEATURES**

### 🔐 Authentication
- User Signup & Login
- JWT Token Authentication
- Secure Password Hashing
- Session Management

### 📸 Content System
- Upload Images & Videos
- Bunny CDN Integration (Fast Global Delivery)
- Auto File Type Detection
- Multi-format Support (PNG, JPG, GIF, MP4)

### 🖼️ Feed System
- Masonry Grid Layout (7 columns → responsive)
- Infinite Scroll Pagination
- Real-time Loading
- Skeleton Loading States
- Smooth Animations

### 👤 User Profiles
- Individual Profile Pages
- User's Posts Display
- Avatar Support

### 🎨 UI/UX
- 100% Responsive (Mobile/Tablet/Desktop)
- Pinterest Red Theme (#E60023)
- Hover Effects on Cards
- Save Pin Functionality
- Toast Notifications
- Modal Dialogs
- Keyboard Shortcuts (ESC, Ctrl+K, /)
- **Logout Button in Header Dropdown**

---

## 🛠️ **TECH STACK**

**Frontend:** HTML5, CSS3, JavaScript ES6+, Tailwind CSS, Font Awesome  
**Backend:** Node.js, Express.js  
**Database:** MongoDB with Mongoose  
**Auth:** JWT + bcryptjs  
**Storage:** Bunny.net CDN  
**File Upload:** Multer + Axios  

---

## 📁 **PROJECT STRUCTURE**

```
pinterest/
├── server.js              # Main server
├── .env                   # Environment variables
│
├── models/
│   ├── User.js            # User model
│   └── Post.js            # Post model
│
├── routes/
│   ├── auth.js            # Auth routes
│   └── post.js            # Post routes
│
├── middleware/
│   └── auth.js            # JWT middleware
│
├── utils/
│   └── bunny.js           # CDN upload utility
│
└── public/
    ├── login.html         # Login page
    ├── signup.html        # Registration page
    ├── index.html         # HOME - Main Feed ⭐
```

---

## ⚙️ **INSTALLATION**

### **1. Install Dependencies**
```bash
npm install express mongoose cors bcryptjs jsonwebtoken multer axios dotenv
```

### **2. Create .env File**
```env
MONGO_URI=mongodb://localhost:27017/pinterest
JWT_SECRET=your-secret-key-here
PORT=5000
BUNNY_STORAGE_ZONE=your-zone-name
BUNNY_API_KEY=your-api-key
BUNNY_PULL_ZONE=https://your-zone.b-cdn.net
```

### **3. Run Server**
```bash
node server.js
```
Visit: `http://localhost:5000`

---

## 🌐 **API ENDPOINTS**

### **Auth**
```
POST /auth/signup  - Register user
POST /auth/login   - Login user
```

**Signup Body:**
```json
{
  "username": "johndoe",
  "email": "john@example.com",
  "password": "password123"
}
```

**Login Response:**
```json
{
  "token": "eyJhbGci...",
  "user": {
    "_id": "...",
    "username": "johndoe",
    "email": "john@example.com"
  }
}
```

### **Posts**
```
POST /post/upload      - Upload post (Auth required)
GET  /post/all?page=1  - Get all posts feed
GET  /post/user/:id    - Get user's posts
```

**Upload Headers:**
```
Authorization: YOUR_JWT_TOKEN
Content-Type: multipart/form-data
```

**Upload Form Data:**
- `file`: Image/Video file (required)
- `title`: Post title (optional)

---

## 📱 **PAGES**

### **1. Login Page** (`/login.html`)
- Email & Password fields
- Stores token in localStorage
- Redirects to feed on success

### **2. Signup Page** (`/signup.html`)  
- Username, Email, Password
- Creates new account

### **3. Home Feed** (`/index.html`) ⭐ **MAIN PAGE**
**Header:**
- Pinterest Logo
- Search Bar (centered)
- Create Button (+)
- Notifications Bell
- Messages Icon
- User Avatar (A) → Click for **LOGOUT dropdown**

**Feed:**
- Masonry Grid (7 columns responsive)
- Pin Cards with hover effects
- Save/Share/More buttons on hover
- User avatars & usernames
- Infinite scroll loading

**Features:**
- Upload Modal (click + button)
- Logout in header dropdown menu
- Toast notifications
- Keyboard shortcuts

---

## 🎯 **HOW TO USE**

### **For Users:**

**1. Register**
- Go to `/signup.html`
- Fill username, email, password
- Click Signup

**2. Login**
- Go to `/login.html`  
- Enter email & password
- Click Login → Redirected to Feed

**3. Upload Pins**
- Click **+** button in header
- Add title (optional)
- Choose image/video file
- Click Upload

**4. Browse Feed**
- Scroll to see all pins
- Hover over pins to reveal actions
- Click **Save** to save pin
- Click username to view their profile

**5. LOGOUT** 🔴
- Click your avatar (**A**) in top-right corner
- Dropdown menu appears
- Click **"Log out"** (red text at bottom)
- Shows "Logged out successfully!" message
- Redirects to login page after 900ms

---

## 🗄️ **DATABASE SCHEMAS**

### **User Model**
```javascript
{
  _id: ObjectId,
  username: String,
  email: String,
  password: String,        // bcrypt hashed
  avatar: String,          // default: https://i.pravatar.cc/150
  createdAt: Date,
  updatedAt: Date
}
```

### **Post Model**
```javascript
{
  _id: ObjectId,
  title: String,
  fileUrl: String,         // Bunny CDN URL
  type: String,            // "image" or "video"
  userId: ObjectId,        // references User
  createdAt: Date,
  updatedAt: Date
}
```

---

## 🚀 **DEPLOYMENT**

### **Quick Deploy (Render/Railway)**
1. Push code to GitHub
2. Connect repo to Render/Railway
3. Set environment variables in dashboard
4. Deploy! 🎉

### **VPS Deployment**
```bash
# Install PM2 globally
npm install -g pm2

# Start server with PM2
pm2 start server.js --name "pinterest"

# Setup Nginx reverse proxy (optional)
# Configure SSL with Let's Encrypt (optional)
```

---

## 🎨 **CUSTOMIZATION**

### **Change Primary Color**
In `public/index.html`, edit:
```css
:root {
  --pinterest-red: #E60023;  /* Change this */
}
```

### **Change Grid Columns**
```css
.masonry-grid {
  column-count: 7;  /* Adjust: 2-10 */
}
```
---

## 🐛 **TROUBLESHOOTING**

| Problem | Solution |
|---------|----------|
| MongoDB connection error | Check MONGO_URI in .env, ensure MongoDB running |
| Upload fails (401) | Verify BUNNY_API_KEY is correct |
| CORS error | Ensure cors() used in server.js |
| Images not loading | Check BUNNY_PULL_ZONE URL |
| JWT invalid error | Clear localStorage, re-login, check JWT_SECRET matches |

---

## 📊 **KEY FEATURES SUMMARY**

✅ **Multi-user authentication system**  
✅ **Image & video upload to Bunny CDN**  
✅ **Pinterest-style masonry grid feed**  
✅ **Individual user profile pages**  
✅ **Responsive design (mobile-friendly)**  
✅ **Logout functionality in header**  
✅ **Infinite scroll pagination**  
✅ **Smooth animations & transitions**  
✅ **Toast notification system**  
✅ **Professional UI/UX matching real Pinterest**  

---



<div align="center">

## ⭐ **Thanks for using this project!**

Made with ❤️ | Powered by Node.js + MongoDB + Bunny CDN

**Happy Coding! 🚀**

</div>


