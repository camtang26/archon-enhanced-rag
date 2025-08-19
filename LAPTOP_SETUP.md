# Archon Enhanced RAG - Laptop Setup Guide

This repository contains Archon with enhanced RAG (Retrieval Augmented Generation) features enabled, including ML-based reranking for the best possible contextual hybrid searches.

## Prerequisites

1. **Docker Desktop** installed and running
2. **Git** installed
3. **Supabase account** with a project created

## Quick Setup

### 1. Clone the Repository

```bash
git clone https://github.com/camtang26/archon-enhanced-rag.git
cd archon-enhanced-rag
```

### 2. Configure Environment Variables

Create a `.env` file in the root directory:

```bash
# Required Supabase Configuration
SUPABASE_URL=your_supabase_project_url
SUPABASE_SERVICE_KEY=your_supabase_service_key

# Optional: OpenAI API Key (can be set via UI)
OPENAI_API_KEY=your_openai_api_key

# Service Ports (default values shown)
SERVER_PORT=8181
MCP_PORT=8051
AGENTS_PORT=8052
FRONTEND_PORT=3737
```

**To get your Supabase credentials:**
1. Go to your Supabase project dashboard
2. Navigate to Settings → API
3. Copy the Project URL and service_role key (not the anon key)

### 3. Build and Start Services

```bash
# Build all services with enhanced RAG features
docker-compose up --build -d

# Check that all services are running
docker-compose ps
```

This will take 10-15 minutes on first build as it downloads:
- PyTorch (~888MB)
- NVIDIA CUDA libraries (~2.5GB total)
- Sentence transformers and other ML dependencies

### 4. Access the Application

Once all services are healthy:
- **Frontend UI**: http://localhost:3737
- **Backend API**: http://localhost:8181
- **MCP Server**: http://localhost:8051
- **Agents Service**: http://localhost:8052

### 5. Initial Setup in UI

1. Navigate to Settings (gear icon)
2. Enter your OpenAI API key
3. Test the connection
4. Start using Archon!

## Enhanced Features Included

This setup includes the following ML enhancements:
- ✅ **sentence-transformers** for advanced embeddings
- ✅ **PyTorch** for neural network operations
- ✅ **transformers** library for model operations
- ✅ **Hybrid search with reranking** for superior RAG results

## Useful Commands

### View Logs
```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f archon-server
```

### Stop Services
```bash
docker-compose down
```

### Restart Services
```bash
docker-compose restart
```

### Update from Repository
```bash
git pull
docker-compose up --build -d
```

## Troubleshooting

### If containers exit on startup:
```bash
# Check logs for errors
docker-compose logs archon-server

# Verify .env file exists and has correct values
cat .env

# Restart services
docker-compose down
docker-compose up -d
```

### If build fails:
```bash
# Clean Docker cache and rebuild
docker-compose down
docker system prune -f
docker-compose up --build -d
```

### Port conflicts:
If you get port binding errors, either:
1. Stop conflicting services, or
2. Change ports in `.env` file

## System Requirements

- **RAM**: Minimum 8GB (16GB recommended)
- **Disk Space**: ~15GB for Docker images and ML models
- **CPU**: Multi-core processor recommended for ML operations

## MCP Integration (Optional)

To use Archon with Claude Code, Cursor, or Windsurf:

1. Install the IDE extension
2. Configure MCP server URL: `http://localhost:8051`
3. Available MCP tools will appear in your IDE

## Support

For issues or questions:
- Original Archon project: https://github.com/coleam00/archon
- This enhanced version: https://github.com/camtang26/archon-enhanced-rag

## Notes

- This setup has ML reranking libraries enabled for optimal RAG performance
- First startup will be slow due to model downloads
- All data is stored locally via Docker volumes
- Supabase is used for vector storage and embeddings