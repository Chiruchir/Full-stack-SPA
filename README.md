# Smarter.Codes Search Application

A powerful semantic search application that allows users to search through website content using advanced vector similarity matching. This application fetches HTML content from any given URL, processes it into meaningful chunks, and returns the most relevant matches based on the search query.

## Features

- 🔍 Semantic search capabilities using vector similarity
- 🌐 Website content fetching and processing
- 🧠 Natural language processing with NLTK
- 💨 Fast and efficient vector search with Weaviate
- ⚛️ Modern React frontend with Tailwind CSS
- 🚀 FastAPI backend for robust API handling
- 🐳 Docker-based vector database
- 📊 Relevance scoring and result ranking

## Prerequisites

Before you begin, ensure you have the following installed:

- Python 3.10+ (3.10 or 3.11 recommended for best compatibility)
- Node.js 14+ and npm
- Docker and Docker Compose
- Git (optional, for cloning the repository)

## Project Structure

```
smarter-codes-search/
├── backend/
│   ├── main.py                 # FastAPI application
│   ├── requirements.txt        # Python dependencies
│   └── .env                    # Environment variables
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── SearchForm.js  # Search input component
│   │   │   └── ResultList.js  # Results display component
│   │   ├── App.js             # Main React component
│   │   ├── index.js           # React entry point
│   │   └── index.css          # Global styles
│   ├── package.json           # Node.js dependencies
│   └── public/                # Static assets
├── docker-compose.yml         # Docker configuration
└── README.md                  # Documentation
```

## Installation

### 1. Clone the Repository (Optional)

```bash
git clone https://github.com/yourusername/smarter-codes-search.git
cd smarter-codes-search
```

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Unix/MacOS:
source venv/bin/activate

# Upgrade pip and setuptools
python -m pip install --upgrade pip setuptools wheel

# Install dependencies
pip install numpy>=1.26.0  # Install numpy first
pip install -r requirements.txt
```

### 3. Frontend Setup

```bash
# Navigate to frontend directory
cd ../frontend

# Install dependencies
npm install

# Install additional development dependencies
npm install --save-dev autoprefixer postcss tailwindcss
```

### 4. Vector Database Setup

```bash
# From project root directory
docker-compose up -d
```

## Configuration

### Backend Configuration

1. Create a `.env` file in the backend directory:

```env
WEAVIATE_URL=http://localhost:8080
MODEL_NAME=all-MiniLM-L6-v2
MAX_TOKENS_PER_CHUNK=500
```

### Frontend Configuration

No additional configuration is needed for the frontend in development mode. For production, you may need to update the API endpoint in `App.js`.

## Running the Application

1. Start the Vector Database (if not already running):
```bash
docker-compose up -d
```

2. Start the Backend Server:
```bash
cd backend
# Activate virtual environment if not activated
uvicorn main:app --reload --port 5000
```

3. Start the Frontend Development Server:
```bash
cd frontend
npm start
```

4. Access the application:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000
- Weaviate Console: http://localhost:8080/v1/console

## Usage

1. Enter a website URL in the URL input field
2. Enter your search query in the search field
3. Click "Search" to find relevant content
4. View results sorted by relevance score

## API Endpoints

### POST /search
- Endpoint: `http://localhost:5000/search`
- Method: POST
- Body:
```json
{
    "url": "https://example.com",
    "query": "your search query",
    "max_results": 10
}
```

- Example Response:
```json
{
    "results": [
        {
            "content": "Relevant content snippet here...",
            "score": 0.95
        },
        {
            "content": "Another relevant content snippet...",
            "score": 0.90
        }
    ]
}
```

## Troubleshooting

### Common Issues and Solutions

1. **Numpy Installation Issues**
   - Solution: Install numpy separately first: `pip install numpy>=1.26.0`

2. **Weaviate Connection Error**
   - Ensure Docker is running
   - Check if Weaviate is accessible: `curl http://localhost:8080/v1/meta`

3. **CORS Issues**
   - Check if backend CORS settings match frontend URL
   - Verify that frontend is calling correct backend URL

4. **Memory Issues with Large Websites**
   - Adjust `MAX_TOKENS_PER_CHUNK` in .env file
   - Consider implementing pagination

5. **Frontend Dependency Issues**
   - Ensure Node.js and npm versions are compatible
   - Delete `node_modules` and run `npm install` again if issues persist

## Performance Optimization

1. **Vector Database**
   - Weaviate data persists in Docker volume
   - Consider adjusting batch size for large datasets
   - Monitor memory usage for large websites

2. **Search Performance**
   - Chunk size affects search granularity
   - Adjust `MAX_TOKENS_PER_CHUNK` based on needs
   - Consider implementing caching for frequently searched sites

## Security Considerations

1. **URL Validation**
   - Frontend and backend validate URLs
   - Consider implementing rate limiting
   - Add authentication for production use

2. **Data Handling**
   - Implement proper error handling
   - Sanitize user inputs
   - Consider data retention policies

3. **Environment Variables**
   - Use environment variables to manage sensitive information securely

## Development Notes

### Backend Development

- Uses FastAPI for async request handling
- NLTK for text processing
- Sentence Transformers for embeddings
- Proper error handling and logging

### Frontend Development

- React with functional components
- Tailwind CSS for styling
- Axios for API requests
- Proper loading and error states

## Production Deployment

Additional steps for production deployment:

1. Set up proper environment variables
2. Configure CORS for production domains
3. Set up proper logging
4. Implement rate limiting
5. Add monitoring and analytics
6. Configure proper security headers
7. Set up SSL/TLS certificates
8. Use a process manager like `gunicorn` or `uvicorn` with workers for the backend

## Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazingfeature`
3. Commit your changes: `git commit -m 'Add amazingfeature'`
4. Push to the branch: `git push origin feature/amazingfeature`
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- FastAPI for the backend framework
- React for the frontend framework
- Weaviate for vector search capabilities
- Sentence Transformers for embeddings
- NLTK for text processing

