# Hackathon Grader

A real-time web application for judging and scoring hackathon projects. Judges can score projects on multiple criteria, and results appear instantly on a live leaderboard.

## Features

### 🎯 Judge Panel
- View the currently active project being presented
- Score projects on multiple customizable criteria (1-10 scale)
- Submit scores with a single click
- Session-based duplicate vote prevention
- Real-time updates when admin switches projects

### 🏆 Live Leaderboard
- Real-time ranking of all projects
- Average scores calculated automatically
- Vote counts per project
- Visual progress bars
- Medal icons for top 3 projects
- Updates instantly as votes are submitted

### ⚙️ Admin Panel
- **Setup Mode:**
  - Add/remove projects and teams
  - Configure scoring categories
  - Initialize hackathon configuration
- **Control Mode:**
  - Select active project for judging
  - View live statistics
  - Reset all votes
  - Reconfigure hackathon settings

### 📋 Rules Page
- Comprehensive hackathon guidelines
- Timeline and schedule information
- Judging criteria explanation
- Scoring system details
- Code of conduct
- Submission requirements

## Tech Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6 modules)
- **Backend/Database:** Firebase Firestore
- **Styling:** Custom CSS with CSS variables
- **Fonts:** Google Fonts (Space Mono, Syne)
- **Deployment:** Static hosting (single HTML file)

## Setup

### Prerequisites
- A modern web browser
- A Firebase project with Firestore enabled

### Firebase Configuration

1. Create a Firebase project at [Firebase Console](https://console.firebase.google.com/)
2. Enable Firestore Database
3. Update the Firebase configuration in `index.html` (lines 599-606):

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.firebasestorage.app",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### Firestore Structure

The application uses the following Firestore structure:

**Document:** `hackathon/config`
```javascript
{
  projects: ["Team Alpha", "Team Beta", ...],
  criteria: ["Innovation", "Technical Execution", ...],
  activeProject: "Team Alpha",
  configured: true
}
```

**Collection:** `votes`
```javascript
{
  project: "Team Alpha",
  scores: {
    "Innovation": 8,
    "Technical Execution": 7,
    ...
  },
  timestamp: 1234567890
}
```

### Firestore Security Rules

Set up your Firestore security rules to allow read/write access:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /hackathon/config {
      allow read: if true;
      allow write: if request.auth != null; // Or adjust based on your needs
    }
    match /votes/{voteId} {
      allow read: if true;
      allow create: if true; // Allow judges to submit votes
      allow delete: if request.auth != null; // Only admins can delete
    }
  }
}
```

## Usage

### Initial Setup

1. Open `index.html` in a web browser
2. Navigate to the **Admin** panel
3. Add projects/teams and scoring categories
4. Click "Save & Start Hackathon"

### During the Hackathon

1. **Admin:**
   - Select the active project from the admin panel
   - Monitor live statistics
   - Switch between projects as presentations occur

2. **Judges:**
   - Navigate to the **Judge** panel
   - Score the active project on all criteria
   - Submit scores (one vote per project per session)

3. **Participants/Viewers:**
   - View the **Leaderboard** for real-time rankings
   - Check the **Rules** page for guidelines

## Project Structure

```
Taiko-Hackathon/
├── index.html          # Single-file application (HTML, CSS, JavaScript)
└── README.md          # Project documentation
```

The application is a single-file SPA with:
- **HTML Structure** (lines 1-592): Page layout and content
- **CSS Styles** (lines 8-495): Dark theme styling with CSS variables
- **JavaScript** (lines 594-925): Firebase integration and application logic

## Key Features

- ✅ **Real-time Synchronization:** All users see updates instantly via Firebase listeners
- ✅ **No Build Process:** Just open the HTML file in a browser
- ✅ **Session-based Voting:** Prevents duplicate votes per project per browser session
- ✅ **Dynamic Configuration:** Admin can set up projects and criteria without code changes
- ✅ **Responsive Design:** Works on desktop and mobile devices
- ✅ **Dark Theme:** Modern UI with gradient backgrounds

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is open source and available for use in hackathons and similar events.

## Support

For issues or questions, please open an issue on the GitHub repository.

---

**Built for hackathons** 🚀
