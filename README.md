# TapIn

TapIn is a comprehensive voice-to-text note-taking application that transforms audio recordings into intelligent, AI-powered summaries. Built with a modern tech stack, it enables users to capture, transcribe, and collaborate on notes seamlessly.

## ✨ Features

- **🎤 Audio Recording**: Record audio directly in the browser
- **📝 AI-Powered Transcription**: Automatic speech-to-text conversion using Whisper AI
- **🤖 Smart Summarization**: AI-generated summaries using Google's Generative AI
- **👥 Team Collaboration**: Create and manage teams with shared notes
- **📊 Note Management**: Organize and access all your notes in one place
- **🔐 Secure Authentication**: JWT-based authentication with cookie management
- **🎨 Modern UI**: Responsive design with Tailwind CSS and smooth animations

## 🏗️ Architecture

TapIn follows a microservices architecture with the following components:

### Frontend
- **Framework**: React 18 with TypeScript
- **Routing**: React Router DOM
- **State Management**: Recoil
- **Styling**: Tailwind CSS
- **UI Components**: Custom components with Framer Motion animations
- **Build Tool**: Vite

### Backend
- **Runtime**: Node.js with Express
- **Language**: TypeScript
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: JWT with cookie-parser
- **File Upload**: Multer for audio file handling

### Transcriber Service
- **Language**: Python with Flask
- **AI Model**: OpenAI Whisper (base model)
- **Audio Processing**: PyDub
- **Queue**: Redis for job management

### Summarizer Worker
- **Runtime**: Node.js with TypeScript
- **AI**: Google Generative AI
- **Database**: Prisma Client
- **Queue**: Redis for background processing

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- Python (v3.8 or higher)
- PostgreSQL
- Redis
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/notsoarsh/Tap-In.git
   cd TapIn-master
   ```

2. **Install root dependencies**
   ```bash
   npm install
   ```

3. **Setup Backend**
   ```bash
   cd backend
   npm install
   
   # Configure environment variables
   cp .env.example .env
   # Edit .env with your database URL, JWT secret, etc.
   
   # Run Prisma migrations
   npx prisma migrate dev
   npx prisma generate
   ```

4. **Setup Frontend**
   ```bash
   cd frontend
   npm install
   ```

5. **Setup Transcriber Service**
   ```bash
   cd transcriber
   pip install -r requirements.txt
   ```

6. **Setup Summarizer Worker**
   ```bash
   cd summarizer-worker
   npm install
   
   # Configure environment variables
   cp .env.example .env
   # Add your Google Generative AI API key
   
   # Run Prisma migrations
   npx prisma migrate dev
   npx prisma generate
   ```

### Environment Variables

#### Backend (.env)
```env
DATABASE_URL="postgresql://user:password@localhost:5432/tapin"
JWT_SECRET="your-secret-key"
PORT=3000
```

#### Summarizer Worker (.env)
```env
DATABASE_URL="postgresql://user:password@localhost:5432/tapin"
GOOGLE_API_KEY="your-google-api-key"
REDIS_URL="redis://localhost:6379"
```

#### Transcriber (.env)
```env
REDIS_URL="redis://localhost:6379"
FLASK_PORT=5000
```

### Running the Application

1. **Start Redis**
   ```bash
   redis-server
   ```

2. **Start PostgreSQL**
   Ensure your PostgreSQL database is running

3. **Start Backend**
   ```bash
   cd backend
   npm run dev
   ```

4. **Start Frontend**
   ```bash
   cd frontend
   npm run dev
   ```

5. **Start Transcriber Service**
   ```bash
   cd transcriber
   python main.py
   ```

6. **Start Summarizer Worker**
   ```bash
   cd summarizer-worker
   npm run dev
   ```

The application will be available at:
- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:3000`
- Transcriber: `http://localhost:5000`

## 📦 Project Structure

```
TapIn-master/
├── backend/              # Express API server
│   ├── prisma/          # Database schema and migrations
│   └── src/             # Source code
├── frontend/            # React application
│   ├── src/
│   │   ├── components/  # Reusable UI components
│   │   ├── pages/       # Page components
│   │   ├── store/       # Recoil state management
│   │   └── utils/       # Utility functions
│   └── public/          # Static assets
├── transcriber/         # Python Flask transcription service
├── summarizer-worker/   # Background job processor
│   ├── prisma/         # Database schema
│   └── src/            # Worker source code
├── common/             # Shared TypeScript types and utilities
└── PDF/                # PDF generation service
```

## 🔑 Key Technologies

- **Frontend**: React, TypeScript, Tailwind CSS, Recoil, Vite
- **Backend**: Node.js, Express, TypeScript, Prisma, PostgreSQL
- **AI/ML**: OpenAI Whisper, Google Generative AI
- **Authentication**: JWT, bcrypt
- **Queue**: Redis
- **Database**: PostgreSQL
- **ORM**: Prisma

## 🛠️ API Endpoints

### Authentication
- `POST /api/v1/user/register` - Register new user
- `POST /api/v1/user/login` - User login
- `GET /api/v1/user/logout` - User logout

### Notes
- `GET /api/v1/notes` - Get all user notes
- `GET /api/v1/notes/:id` - Get specific note
- `POST /api/v1/notes` - Create new note
- `PUT /api/v1/notes/:id` - Update note
- `DELETE /api/v1/notes/:id` - Delete note

### Teams
- `POST /api/v1/teams` - Create team
- `GET /api/v1/teams` - Get user teams
- `POST /api/v1/teams/:id/members` - Add team member
- `GET /api/v1/teams/:id/notes` - Get team notes

### Transcription
- `POST /convert` - Convert audio to text

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 👥 Authors

- **Deepshikha1211** - [GitHub](https://github.com/Deepshikha1211)

## 🙏 Acknowledgments

- OpenAI Whisper for transcription capabilities
- Google Generative AI for summarization
- The open-source community for amazing tools and libraries

## 📧 Contact

For questions or support, please open an issue on GitHub or reach out through the contact page in the application.

---

Made with ❤️ by the TapIn team